---
layout: post
title: A Shade of turquoise
categories: [work]
published: true
---

During a conversation with one of my coworkers, I brought up something about doing a blue/green cutover for one of our apps when we go to production.   He responded, "That's stupid and we should just do it the old fashioned way."   I was taken aback by the statement, but then I really got to thinking about it....

FACT 1: If you are writing an app that runs in or depends on public cloud stuff at all, it is up to you to make sure it is resilient to failures.  There will be failures.   You don't have access to control everything in the infrastructure or the network, so you need to build in your own resiliency to those problems.  

FACT 2: Everyone knows computers and software are unreliable. 

FACT 3: Very few applications are so critical that they cannot take a blip, or even a fairly extended blip, of downtime.  From the smallest company to the largest, the costs invoked due to downtime are often overblown.  I've been at a grocery store when the point-of-sale system went down.   Know what?   People either waited for it to come back up or they left.  Whatever was in their carts was either put away or thrown in the garbage by the employees of the store, and then, guess what, everything came back to normal.  Those who left their stuff came back another time and got it.   No one was mad, which kinda goes back to FACT 2.

FACT 3: Your system is not that important.  Very few systems need to be upgraded in a blue/green kind of way without downtime. If you're monitoring anesthesia at a hospital, then sure.  If you are watching nuclear weapon storage, then fine.  If you are supporting the oxygen systems in the ISS, the of course.   But I cannot think of everyday businesses that need that level of uptime. 

So the more I've thought about it, the more I think he is right. As an old IT pro, it's hard to say, "Downtime is fine" and feel good about it.  Downtime IS fine, though.  As long as it's expected and the work is reasonably planned.  