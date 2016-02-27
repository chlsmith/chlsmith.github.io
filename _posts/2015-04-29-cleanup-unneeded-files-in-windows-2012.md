---
layout: post
title: Cleanup Unneeded Files in Windows 2012
date: 2015-04-29 08:33
author: chlsmith
comments: true
categories: [Uncategorized]
---
Back in the day, I used to copy the i386 directory from the CD to any computer I stood up.   This allowed me to use these files to install new features, such as printers or whatever, down the road.   Nowadays, these files are stored under c:\windows\winsxs, and this "store" is updated every time a new component or update to a component is installed.   Over time, it grows, and sometimes I just don't have the space to save all that stuff.   Even the files for the features I don't use are there, just in case I want them.

I found a nice little article today with a command that cleans that up.   The command, when run from an elevated command prompt, will automatically go through and remove any of the old files that have been replaced with newer versions, and in the case of Windows 8.1 or 2012R2, you can actually remove everything else easily.   The ResetBase only works on 8.1 and 2012R2.

dism.exe /online /cleanup-image /StartComponentCleanup [/ResetBase]

This takes a while, but eventually completes and saves you a bunch of space and maybe saves your day.
