---
layout: post
title: Windows Update with DSC
date: 2015-06-30 08:26
author: chlsmith
comments: true
categories: [Uncategorized]
---
Funny thing with the DSC resource kits, provided by Microsoft.   There isn't a resource to configure Automatic Updates on a machine.   There's an update resource there, but it's simply to check for and to install a single update.    Time to write my own!

I went onto one of my machines on the domain, that is configured via GPO to check for updates from my WSUS server.   I exported the registry key located under HKLM:\Software\Policies\Microsoft\Windows\WindowsUpdate, and decided that all I needed to do was create a resource to check for and to set these options.

I got the base Get, Set, and Test options configured pretty easily, but the problem is now that even with these registry settings in place, my test machine won't check for the updates.   Weird.   More to come.
