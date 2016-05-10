---
layout: post
title: Simple Discovery
categories: [powershell]
published: true
---

Powershell can be picky.   I discovered this the other day, when I was trying to run some DSC resources that I had on a computer.  I kept getting an error that the module was installed in more than one place, and I needed to specify the right one to use.  I dug through all the normal places Powershell modules are, and they were only under "c:\program files\windowspowershell\modules", as they should have been.  I ran get-module to find out where it was, and both were listed under the same directory.

WTH?  After deleting and recreating the module folder and some other general head banging on my desk, I checked out the PSMODULEPATH variable.   Lo and behold, for some reason the path to the modules was in the variable twice.  When I was starting Powershell, it was reading the module in two times, even though it was only there once.

I still don't know how I got the path variable messed up.  That's two hours I'd like to have back.