---
layout: post
title: Doing Things Right in the Cloud
categories: [opinion, tech]
published: true
---

The cloud exposes a lot of laziness and cheapness on the part of IT teams.  When you no longer have control of underlying hardware, you can no longer work around your own system design flaws.   A perfect example of this is highly available SQL Server.  Should you always build your DB servers so if one goes down, the others keep things running?   OF COURSE, but there are cost constraints (think doubling your hardware and going up a version of SQL Server) that often leave people running only one SQL server.  This doesn't just apply to physical db servers, either...it's true of virtual ones.  If you're patching your VMware hosts, you have the control to make sure all the VMs are moved off of them as you restart the hosts, thereby keeping your VMs running.

When you go to the cloud, you don't have control of the physical machines or the hosts anymore.  If the folks running Azure or AWS need to patch or reboot their hosts, they cannot have their hands tied to calling every customer to move their VMs.  Their engineers can't sit through every customer's change management meeting to get the updates approved.   They can't reboot at a "convenient" time, because their stuff is running 24/7.

What do they do?   They simply tell you when it's going to happen and do it.  What does that mean?   If you've been cheap and not built your VMs up into a highly available group, you are going to take an outage.  As a matter of fact, Microsoft gives you no SLA if you only have a single VM instance running for an app.

What can you do?   You can build your stuff RIGHT in the first place.  You need a highly available database server?   You need to research that and make it happen...you can't just wing it and work around your own cheapness.  You want your web server to have five 9's of availability?   You need to set up at least a pair of servers and load balance between them.  The same is true for every single service you plan to provide.  Do it right or you're going to have problems.  Don't blame "the cloud"....you should've been doing it this way the whole time.