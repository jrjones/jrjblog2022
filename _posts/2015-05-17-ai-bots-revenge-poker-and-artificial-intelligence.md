---
layout: post
title: "Revenge of the Bots: Poker &amp; AI"
date: 2015-05-17 22:18
categories: [Poker, Futurism, Technology]
tags: [artificial intelligence, machine learning, futurism, game theory, poker, research, technology]
author: jrj
teaser: "A look at trends in poker AI, and predictions on impact over the next decade…"
image:
  src: "/images/postheads/pokerai.png"
  width: 100%
  homepage: "postheads/pokerai.png"
  thumb: "postheads/pokerai.png"
header:
  image: "postheads/pokerai.png"
  background-color: "#333333"
---
<!---
![Poker AI](/assets/postheads/pokerai.png "Poker AI")
-->
Early on in my poker playing “career” (before legislation passed in my then home state of Washington that made playing online poker a felony) I played frequently online. One of the trends I started to notice was that a small trickle of poker “bots” were starting to be used. Players would deploy software to play on their behalf, and these “bots,” simply through a combination of very tight play and the horrible loose-passive opponents at micro-limits, could apparently eke out small win rates (which, when multi-tabling 24/7 could presumably add up to enough money to offset the cost of the bot.) However, their play was atrocious. I remember reading articles at the time with tons of hand-wringing about these bots, but they didn’t bother me. Indeed, I maintained a list of players that I suspected were bots and sought them out—they were predictable and highly exploitable. I would find one playing, and wait for the seat to its left to open up, and grind out nice profits at their expense. It was fun, and I enjoyed knowing that I was harming the already pathetic win-rate of unscrupulous players who were using software that was clearly against the terms of service of the site (AKA “Cheating.”) None of the accounts lasted very long, so I suspect that the bots were actually losing money in the long run, and consequently fell into disuse. Also, poker rooms started deploying countermeasures and looking for evidence of bot use, and suspending accounts. Fast forward almost a decade, and what was once an amusing and exploitable novelty may now be morphing into a legitimate threat.

2015 has been a momentous year for the development of artificial intelligence and the game of poker with huge accomplishments by researchers. Unfortunately, as is so often the case with complex subjects, the mainstream media has done a horrible job of reporting these developments, usually vastly overstating them. Publications focused on AI have done a poor job of reporting these developments because of a lack of poker understanding, and poker writers have done an even worse job due to a lack of general AI knowledge. I thought I might share some thoughts on the current state of poker AI research, and how I expect it will impact the game of poker in the coming decade.

In late 2014 and early 2015, the Internet was hyperventilating over [a paper published by the AAAS journal Science](http://www.sciencemag.org/content/347/6218/145.abstract). Most of the confusion came from the published title of the paper (“Heads-Up Limit Hold’em Poker is Solved”) which I believe to be misleading. Since nobody reads the actual articles (let alone academic papers) the mainstream press pressed hard on the hyperbole accelerator pedal, stating [that poker had been solved](http://www.slate.com/blogs/future_tense/2015/01/14/two_player_heads_up_limit_texas_hold_em_poker_weakly_solved_by_ai_researchers.html), often [comparing it to IBM's Deep Blue](http://www.cbc.ca/news/technology/heads-up-limit-texas-hold-em-poker-solved-by-university-of-alberta-scientists-1.2893987)’s stunning [victory over chess champion Gary Kasparov in the late 90s](http://en.wikipedia.org/wiki/Deep_Blue_versus_Garry_Kasparov). However, nothing like that has actually occurred. Yet.

# Specific and esoteric variation of Poker

First of all, this was a very specific game type: Heads-Up Limit Hold’Em (which I will abbreviate from here on out as HU-LHE.) This is a game that, by and large, humans don’t play. Even before this paper was published, it would have been impossible to find this game being spread in any bricks-and-mortar casino, and you’d likely be unable to even find such a game actively played on any of the myriad online poker sites. Heads Up (2-player) Limit (structured betting with fixed limits) Hold’Em (A stud variation with 2 hole cards and 5 community cards) just isn’t a game humans play in the real world. It’s essentially the simplest form of poker—artificially so. It’s a convenient simplification that exists for two reasons:

* To facilitate research exactly like this—by evaluating a simplified subset of the game of poker, researchers (and the game engine they create) have a more tractable problem to solve. By limiting to two players, you drastically simplify the game—easily by an order of magnitude or more. However, by using structured betting (typically a small blind that is ½ of the big blind, a “small bet” during the first 2 betting rounds equal to the big blind, and a “big bet” in the later betting rounds of double the big blind) instead of pot limit or no-limit, you’re drastically limiting the number of possible actions per betting round. Anyone with even a passing familiarity with poker would say that HU-LHE is several orders of magnitude less complex than the more common 6-10 player games with no structured betting limits (No Limit Hold’Em, abbreviated NLHE.)

* To create poker machines for casinos to replace the familiar video poker that plays outdated draw poker with something that looks more like what modern players see on TV without exposing the casino to undue risk.[^1]

# Solved? Not quite.

So the stories that showed up in the first half of this year that suggested online play would no longer be playable were wrong, even if based solely on evaluating only the title of the paper in question. However, when you dig into the abstract ([still available without paying for the journal](http://www.sciencemag.org/content/347/6218/145.abstract), by the way) you find that even restricting the statement to just the one game (that, again, humans don’t really play) isn’t enough to eliminate the hyperbole.

To quote the abstract: (emphasis added)

> “…Whereas many perfect-information games have been solved (e.g., Connect Four and checkers), no nontrivial imperfect-information game played competitively by humans has previously been solved. Here, we announce that heads-up limit Texas hold’em *is now essentially weakly solved*”

*“Essentially weakly solved.”* That sounds like a lot of wiggle-words, but if you read the paper they are reasonably well qualified and defined. However, very few of the mainstream articles I read used this language in the title or even the first few paragraphs. Most of them repeated the paper title’s flawed assertion that the game was “solved.”

So what does this mean? Well, first let’s start with the objective, mathematical term “weakly solved,” which comes from a branch of mathematics called [Game Theory](http://en.wikipedia.org/wiki/Game_theory).

A game that is [weakly solved](http://en.wikipedia.org/wiki/Solved_game#Weak) means that an algorithm is capable of ensuring a win or a draw for the player—the “weak” solution ensures that the player will not lose. However, a weak solution does not ensure optimal play against an imperfect opponent.

A [strongly solved](http://en.wikipedia.org/wiki/Solved_game#Strong) game means that an algorithm exists that can produce perfect play, even if mistakes have already been in earlier moves/plays by either side. "Strong" proofs are often generated and/or proven by brute force analysis,[^2] where a computer exhaustively searches an entire game tree to evaluate all possible branches. Perfect play would punish mistakes from the other player(s) and ensure no exploitable weakness on the part of the algorithm player. Blackjack is a strongly solved game, as is the aforementioned Tic Tac Toe.

In a simple game like Tic-Tac-Toe, the difference between weakly and strongly solved games is largely academic. However, the difference is huge in a complex game. Optimized play against an imperfect opponent can mean the difference between losing money and earning it in a game like poker.

So HU-LHE is weakly solved? No, not quite. They said “*Essentially* weakly solved.” Unfortunately, that wiggle-word is a bit more subjective. The authors of the paper take care to define it thusly:

> The result is that our new program Cepheus is beatable for […] 0.05 BB/100. Even if you knew the perfect counter-strategy and could play it flawlessly, it'd take 60 million games to overcome the variance due to luck in order to actually have 95% confidence that you were winning. It's essentially solved: not quite perfect, but closer than any human could distinguish within a lifetime of play.

This is pretty dense prose, but it’s clear and unambiguous. The current algorithm is technically beatable by perfect play, but with such a small win rate that, given expected variance, no human could reliably beat it within the number of hands that can reasonably be played in a single human lifetime. While a lot of poker experts quibble about this terminology, I think it’s reasonable and well defined. Hence, the “essentially” wiggle-word is academically interesting and important from a scientific perspective, but is not important from a practical perspective.  Put another way, there’s no approximation in math—if X=1 but you get the answer 1.000000000000001, your algorithm is objectively wrong. However, how meaningful that precision is in practice depends on the application. What the authors are saying is that while their algorithm can technically be beaten (X!=1) it can only be beaten “in the long run” where “long” is equal to a duration greater than a human lifetime. Their algorithm does not technically achieve the [Nash equilibrium](http://en.wikipedia.org/wiki/Nash_equilibrium) required for a true solution to a game of imperfect information, but it gets close enough that it doesn’t matter from a practical perspective against human players.[^3]

OK, so where does that leave us? Is poker solved? No, a highly specialized (and simplified) version of poker that humans don’t really play is essentially weakly solved to the extent that no human player can reliably beat it, but it will not be able to extract money from the best players. It’s not playing an optimized game, and does not know how to maximally exploit suboptimal play from its opponent.

Another tidbit that I think is important is that the researchers acknowledge that the algorithm does not take its opponents past actions into account. Each hand is essentially an independent game, with no history. At the risk of oversimplifying, the algorithm simply looks up the current hand and board combination in a giant database[^4] and gets the answer of how to act with no regard for its opponent’s past actions. This makes sense, since they are seeking a Game Theoretical Optimal (GTO) solution, so they want actions that are not exploitable. However, it’s a terrible way to maximize winnings at the poker table.

# Moving the Research Forward
Where does this research go from here? Presumably in two directions in parallel, ideally converging in a few years.

First, poker playing algorithms need to develop the ability to play No Limit games. This will geometrically increase the size of an already massive dataset, but probably still within a size manageable by modern research-grade computing. (Going from ~17 terabytes to a few petabytes doesn’t make this problem intractable to researchers. Indeed, the researchers already have a no-limit version, which can beat a typical novice player, and it will continue to improve. Another by strong players, but with too small a sample size to be statistical proof.[^5] I suspect that they will be able to claim that HU-NLHE will be “essentially weakly solved” within 1-3 years by simply applying their current HU-LHE methodology with moderate but achievable increases in storage and CPU requirements to handle the additional permutations, and playing a few trillion more hands to better tweak the algorithm will also help.

Second, poker playing algorithms need to get to a point where they can play against multiple opponents. Playing against a single opponent is obviously (and precisely) an order of magnitude more complex than playing against 10. However, I would argue that the subtleties of the game, and actions of each player impacting the decisions of players left to act make 10-handed Limit Hold’em (a game that is popular and commonplace in both online and bricks-and-mortar poker rooms) significantly more than simply 10X more complex than vs. a single opponent: players interact with one another in ways that start approximating [graph theory](http://en.wikipedia.org/wiki/Graph_theory). If you accept the graph of those interactions at face value, it’s not 10X more complicated, **it’s theoretically 1,000 times more complicated.** However, it’s probably not quite that much of an explosion in practice[^6], and a well designed algorithm can probably compress that significantly. I’m guessing somewhere in the 20-60X range. That’s not a problem that’s within the reach of current researchers without significant increases in funding or computational power at a given price point. Assuming funding as a constant, that’s 5-7 doublings of computational power, or ~7-10 years of Moore’s Law if you assume the researchers’ current techniques.

However, I strongly suspect that the application of *deep machine learning* techniques can be successful much faster. Rather than a simple “regret score”[^7] on each of trillions of hands, machine learning can extrapolate meaningful insights beyond simple brute force trial and error, and with less computational power.[^8] Of course, even a strongly solved algorithm would be vulnerable to on the part of its human opponents. Even theoretically perfect play can only beat multiple opponents who are not colluding against the computer, even implicitly. [^9]

My back-of-the envelope calculations put us at 1-3 years away from HU-NLHE being “effectively weakly solved,” and probably another 3-5 years on top of that for full ring games of 6-10 players (with a small possibility it could take as much as 10 years.) So how does that impact the poker world?

# Can online poker stop bots?
Even today, every online poker room I am aware of prohibits the use of poker algorithms that play the game or instruct the player what actions to take. However, I don’t see how a poker room could effectively enforce a ban on artificial intelligence software.

- **HU-LHE:** From a practical perspective, Heads Up Limit Hold’em is already weakly solved. It will be impossible for even the best player in the world to beat a well-designed algorithm. Hence, human players should steer clear of online HULHE games, which they already do. So this is academically interesting, but has no real practical impact beyond creating a bunch of press.

- **HU-NLHE:** Heads Up No Limit Hold’em will likely be essentially weakly solved within the next couple years. Current algorithms, while not quite at the level of game theory optimal, can likely beat typical low-limit players. Unless you are a world-class player, you should probably consider gradually moving away from heads-up online play (except as the end of final table play in a tournament.) Within a couple years, that recommendation will apply to expert and world-class players as well. Heads-up online play has a short shelf life.

- **LHE:** 6-10 handed Limit Hold’em is probably safe for now, but I expect typical players to be beatable by bots within the next year or two, and world-class players in 3-5 years.

- **NLHE:** 6-10 handed No Limit Hold’em, often referred to as the “Cadillac of Poker,” is the game that decides the World Series of Poker Main Event. Based on the pace of current research, I expect this game to be “essentially weakly solved” in the next 5-7 years. This means that online poker may not be able to survive the bot onslaught beyond that point with its game integrity intact. I will be surprised if online poker still exists at the current scale in 7 years, positively shocked if it lasts 10 years. However, I sincerely hope I’m wrong about that.

These estimates are for how long before research-grade computing will take to get to the described levels of play. This means fairly substantial computing resoruces. However, keep in  mind that through cloud hosting platforms like Amazon’s AWS and Microsoft’s Azure, virtually unlimited computing power is available to anyone for a price. However, that price is fairly high today—perhaps adding a couple years to each of my estimates for high-end desktop computers to catch up with the resources required would be reasonable.


[^1]: When you play poker in a casino, you aren’t playing against the house, you’re playing against the other players. The house takes a small amount out of each pot, called the “rake.” This means that poker represents zero risk to the casino; they make money on every hand. That’s why with video poker machines you are playing a variant of poker with no other players, simply trying to achieve a 5-card poker hand. This presents a simple statistics problem that the house can maintain a standard and predictable edge. The simplicity of HU-LHE allows them to create video poker machines with a game that looks more like the game players see on TV, but where the casino can ensure it can’t be consistently beaten by skilled players.

[^2]: One of the best ways for someone with even a beginner’s programming knowledge to understand game theory brute force analysis is to take a look at the [GarboChessJS engine](https://github.com/glinscott/Garbochess-JS), which is an incredibly strong chess algorithm implemented in [~2500 lines of surprisingly readable JavaScript](https://github.com/glinscott/Garbochess-JS/blob/master/js/garbochess.js). Very fun to read, if you’re into that sort of thing. You’ll be amazed (and, if you play chess, humbled) by how simplistic it is.

[^3]: Also, the algorithm is playing without a “rake,” making it a zero-sum game. Add a rake and the algorithm would not be able to force a win/draw, but it would ABSOLUTELY be able to prevent the other player from winning money sufficient to beat the rake.

[^4]: No, I mean _really_ big. Through compression and elimination of redundant card combinations that are equivalent from a practical perspective (for example, it needn’t care if your AQs is spades or hearts) **they were able to reduce the data set down to 11 terabytes for counterfactual data, and 6 terabytes for main strategy data.** Yeah. That’s a lot of ones and zeroes. Using it in practice required 200 computational nodes, each with 24 CPU cores and 32 gigabytes of RAM *each*. Don’t expect to see an iPhone version until a few dozen more doubling cycles of Moore’s Law have kicked in.

[^5]: The win rate had the human players positively crushing the computer with a win rate of over 9BB/100 hands, but with only 80,000 hands played, statisticians are rightfully calling “LOLsamplesize.”

[^6]: A player’s decision when holding middle-strength cards is profoundly impacted by the actions of other players and players yet to act, but extremely weak or strong holdings often play the same regardless of what your opponents do in full ring games.

[^7]: The Cepheus algorithm is largely designed around minimizing its regret: it reviews every decision and then learns which ones paid off, and which ones cost it money. However, unlike human players, this analysis is not colored by selective memory or faulty statistics.

[^8]: Some interesting deep learning resources: Google’s [DeepMind](http://www.wired.com/2015/02/google-ai-plays-atari-like-pros/), IBM’s [Watson](http://en.wikipedia.org/wiki/Watson_(computer)). Also, check out [this TED talk for a great visual introduction](https://www.youtube.com/watch?v=xx310zM3tLs) to the concept. (OK, Watson is arguably not technically deep learning, but it uses substantially similar techniques from the perspective of how one might train a poker bot.)

[^9]: Even a “strong” solution algorithm could only beat players who are not playing together/colluding. If you assume the use of an algorithm/bot is cheating (and it is) then players could cheat in response. However, the resulting game is completely lacking in integrity, and loses all interest.
