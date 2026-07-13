---
layout: post
title: "Submitted to App Store: WiFi Analyzer 2.0"
date: 2026-06-30 08:00:00
tags: [iOS, rimrock-systems]
author: jrj
---
I guess I'll toggle my title from "Retired" to "Semi-retired." (I've been wanting to tinker with iOS apps for coming up on 20 years now.)

A while back, I acquired a small iOS app named "[WiFi Analyzer: Network Master](https://wifimaster.app)" because I wanted to learn my way around Apple's App Store ecosystem. I chose this app because every time I connect to a new network (at a coffee shop, AirBnB, etc.) I always do a quick speedtest and network scan, so I knew I'd use the app almost daily, which to me is a must for a solo dev. This was just step 1 of many: I have a bunch of apps of dubious commercial value that I simply want to exist. With this app in the store, I can now start building those. 

The acquisition completed just in time for us to plan and execute a cross-country move from North Carolina back to Arizona Rim Country, which took a lot longer (and was more all-encompassing) than I expected.

Anyway... I finally got around to shipping the ground-up rewrite of the app. I removed all the third-party trackers.* 

I also added a bunch of "ground-truth" tests to compare the results from the network scanner to what typical UNIX tools find on the Mac, so the scanner is faster and more accurate. 

Then I added initial iPad, MacOS, and VisionOS versions, we'll iterate towards more native implementations on each platform.

The speed test was using public servers that were unreliable, so I added 4 private nodes just for my app that are much more reliable and have plenty of capacity. Then I added a service that looks at all the public servers from each of those vantages and filters to just servers that seem to be responding well. 

I still have a ton of work to do, and I'm still waiting for App Store ~~rejection~~ **approval** but I'm pumped that it's actually MY app there now instead of the vibe-coded monstrosity I acquired. (I was not planning to do a ground-up rewrite, I was planning to just remove the third-party trackers... but it was just so awful I just went file->new project.) 

Next update will add localized versions in a few languages, then I'll add right-to-left languages in a later release. Also, this is basically a clone of the old app with a modernized UI so now it's time to actually add real features and functionality (I knew I couldn't remove any features with paying users.)

A lot of interesting stuff in getting here from there, I plan to write up the network operations and testing stuff once the updated app is fully released. 

(Don't download 1.0 - seriously. Wait until 2.0 is approved.)

---

\* Edited July 13, 2026: this post originally said 2.0 also reduced the pricing and removed the free-trial dark pattern. It didn't — the old pricing remained in 2.0 by mistake, and was fixed in [2.1](/2026/07/13/a-promise-only-i-noticed-i-was-breaking/).