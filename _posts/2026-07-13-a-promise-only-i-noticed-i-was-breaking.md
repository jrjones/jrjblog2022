---
layout: post
title: "The promises I was quietly breaking"
date: 2026-07-13 08:00:00
tags: [iOS, macOS, visionOS, rimrock-systems]
author: jrj
image: /assets/img/wifimaster-2-1/visionos-dark-museum.png
---
<a href="https://wifimaster.app"><img src="/assets/img/wifimaster-2-1/wifimaster-icon-dark.png" alt="WiFiMaster app icon" width="96" class="left" style="border-radius: 22.37%;"/></a>

When [WiFiMaster 2.0 shipped](/2026/06/30/app-store-upload-wifimaster/), it was designed for iPhone but "ran fine" on iPad. (It felt like a big phone, but it worked.) The app also ran on Mac and Apple Vision Pro on day one, technically. Both of them ran the "Designed for iPad" build: a tablet-shaped, blown-up iPhone app in a window, pretending. The whole pitch of [Rimrock](https://rimrocksystems.com) is native craft, yet here I was shipping the exact thing I hate, on two platforms at once. Fortunately, that state of affairs lasted less than 2 weeks.

**Today [version 2.1](https://apps.apple.com/app/id6615082791) was approved.** The Mac version is a real Mac app now, with a resizable window and a sidebar, a real menu, keyboard shortcuts for scanning and exporting, a menu-bar extra that runs a scan or a speed test without opening the window, a sortable table of devices with an inspector, export, print, undo. It behaves like Mac software because it finally is Mac software. There's still a lot of work here (I'm looking at you, iCloud Sync) but at least it's not a phone inside a tablet inside a Mac anymore.

![Speed test history in the native Mac app](/assets/img/wifimaster-2-1/mac-speed-history.png)
_Speed test history, in a real Mac window._

**The Vision Pro version is now a native visionOS app** instead of iPad compatibility mode. It supports native charms, and the translucency that makes it feel at home in the headset. I've tested it on an M2 and M5 Vision Pro, and can't tell the difference (from here on out, the M2 is the target I'll test on as primary so I have a good sense of performance. The M5 is too fast for performance testing.)

![WiFiMaster's Speed Test running natively on Apple Vision Pro, floating in a dark museum gallery](/assets/img/wifimaster-2-1/visionos-dark-museum.png)
_[WiFiMaster 2.1](https://wifimaster.app), running natively on Apple Vision Pro._

**I also spent some time on the iPad version.** I did this one last, by design. With the iPhone version baked, and the full-featured Mac version in place, iPad had permission to find the happy balance that better fits its form factor.

<div style="display: flex; gap: 1.5rem; flex-wrap: wrap; align-items: flex-start;">
  <img src="/assets/img/wifimaster-2-1/ipad-speed-dark.jpg" alt="Speed test on the rebuilt iPad app" style="flex: 1 1 300px; min-width: 0; border-radius: 14px; box-shadow: 0 6px 12px rgba(0,0,0,0.5);"/>
  <img src="/assets/img/wifimaster-2-1/ipad-inspector-dark.jpg" alt="Device table and inspector on the rebuilt iPad app" style="flex: 1 1 300px; min-width: 0; border-radius: 14px; box-shadow: 0 6px 12px rgba(0,0,0,0.5);"/>
</div>
_The rebuilt iPad layout._

**How I got there, if you care about process:** port to the hardest surface first. The Mac is the least forgiving of the three, so I built there, learned what the design actually wanted, and pushed those lessons back down to iPad and iPhone. Hard-platform-first pays for itself twice. And it gave me a huge backlog of ideas for future versions, including a rebrand.

## The uncomfortable part
I mentioned in the [2.0 release post](/2026/06/30/app-store-upload-wifimaster/) that the app was an acquisition, and my first task was removing third-party trackers and shipping a ground-up rewrite that doesn't phone home to data brokers. The part that didn't happen until 2.1 was changing the pricing model.

I'm not going to sugar-coat it... the app was borderline scammy. It was pushing users to an absurdly expensive weekly subscription with a free trial, in hopes it could collect rent on those that forgot to cancel. *That ends today.*

**Now the app is a ~$10 one-time purchase**, or if you prefer, a $2/mo subscription. That $10 is less than 2 weeks of the previous weekly price, but it's more representative of the app's functionality.

Also, instead of a paywall at the beginning of the app, **I want to make this a genuinely useful free app.** *The only thing that is blocked in the free version is speed tests against Rimrock private servers because that costs me actual money.* Free users get 3 private speed tests a week, but can run as many as they want against public servers. (Public servers are less reliable and collect logs. My servers only hold 72 hours of logs, and even those are anonymized... and they are *reliable*.)

**With 2.1 the transition from acquired app to Rimrock product is complete. This is a product I can stand behind and continue to improve on, and it's a pricing model that's much more up front and fair.**
