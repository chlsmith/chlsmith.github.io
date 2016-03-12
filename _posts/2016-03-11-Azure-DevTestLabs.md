---
layout: post
title: Azure DevTest Labs
categories: [cloud]
---

Raise your hand if you've ever decided to take a bunch of old computers and repurpose them as a test lab. Not your mousing hand, fool, the other one.   Okay.....

After virtualization became common, did you throw away the old hardware and just spin your test systems up either on your local computer or secretly on some hardware at your office?  Admit it...you did.

Now that cloud IaaS is so common and cheap, I bet you're doing that there now. You might even be using some Azure credits for it through your subscription.

As a provider of services to your IT department, wouldn't it be nice to just be able to hand all of your folks their own little lab to play with, yet have some control over how much you spend on it?  "Azure DevTest Labs" is the solution.  Currently in preview, DevTest Labs are an Azure V2 solution that allows subscription administrators to carve up a little chunk of cloud and assign it to a user or team.  The admin can drop some custom operating systems into the lab, configure limits on the number of virtual machines (VMs) users can build and their sizes, and then just let the users have at it.   They can spin up, delete, stop, restart, log into, and break as many VMs as their lab allows, and it's completely segmented from everything else you have in the subscription.

There's a slick artifact deployment setup on the labs, too.  You can upload artifacts, or use some that are provided, and have them load into the VMs when they're built.  For example, you can deploy a Chocolatey application to your VM machines automatically.  Neat.

As this is still in preview, there are things that aren't quite ready.  At this time, there's no way to capture images from the VMs that are there, which is kind of a drag. There are also no Microsoft-provided client OS (Win7, 8, 10) images, so as an admin you have to provide those yourself.   If you do have custom images to hand out, getting them there isn't particularly obvious.  (Here's the trick....you have to figure out the storage account used for the lab and then upload your VHDs into the "uploads" container in that storage account.)

As it stands, DevTest Labs are a really nice replacement for the old stack of computers under your developers' desks.  There are some things still needed, but I've heard from good sources that they're coming.  This should be a nice little solution to get some good use out of in the near future.