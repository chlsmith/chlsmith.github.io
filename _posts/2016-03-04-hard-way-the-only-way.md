---
layout: post
title: The Hard Way is the Only Way
categories: [work]
published: true
---

I hate to admit it, but sometimes the only way to get something done is to do it the hard way. Last week, I had an issue where I need to roll out a change to every one of my Chef clients.  The change was to switch the Chef client from running as a service to running as a scheduled task.   I created a recipe that would stop and disable the service, then schedule the task.  After some local testing, I found that it worked and was ready to roll out.

The only problem was that the service on my clients wasn't checking in reliably.   How would I push out the new configuration in a timely fashion if the check-in isn't happening?  My first instinct was to think about rebooting everything and hoping the Chef service would check in on reboot. Obviously, I can't just reboot everything on a whim, but I can restart the Chef service.   I wrote up a quick PowerShell script to do just that.   Run from my management jumpbox, I used "invoke-command" against everything. Sadly, while I was able to restart the service everywhere, that didn't force the check-ins.

That left me only one option: touch 'em all. I simply logged into each machine and ran chef-client to force a check-in. It took a while, but it was a valuable exercise.  I found a few machines that weren't connecting right at all, so I was able to fix those.   I found a couple of my recipes had quit working, so I redid those. I also updated some of my Chef clients to the newest version, as they were really old. I even cleaned up a few recipes that were getting some innocuous errors.

It took a lot more work, but having to go through one-by-one started me on a trajectory that left me at a better state than when I started. Now things should work right for at least another 6 months.