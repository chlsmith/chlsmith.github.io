---
layout: post
title: Linux as My Desktop
categories: [linux]
published: true
---

Last week, for some reason, I decided to install Linux on my laptop and use Windows within a VirtualBox VM.  I have had VirtualBox on Windows and had an Ubuntu VM running there for a while, but I really never used it.  I decided to do the old fliparoo on that, just to see where it took me.

Ubuntu is easily installed and I did a plain-old "desktop" installation.   I don't know enough or even care enough to start with nothing and add only that which I need.  I just wanted something that worked.  After installation, I was on the quest to find my apps.   Luckily enough, I use a lot of open source apps anyway, and they all had Linux versions.  

Chrome, VLC, Slack Desktop, Keepass, VirtualBox, VS Code (which is slick as hell, btw), and a remote desktop app were all easily found.   I did have some issues getting the built-in Remmina Remote Desktop to work with the remote desktop gateway, but by updating xfreerdp, it started working.

The only daily apps I don't have are Outlook, Skype for Business, and PowerShell.  Outlook is easily replaced with Outlook Web Access, which with Office 365 is really nice.   I use PowerShell primarily to build and maintain my Azure machines, so I loaded all the necessary modules into my VirtualBox VM and onto my jumpbox in Azure, so I'm covered there.   The only can't-live-without app that I have to run on Windows is Skype for Business.   Skype itself has a Linux client that looks really nice, and according to some notes on it, you can connect to Skype for Business users with Skype on Windows or a Mac.   That doesn't work on Linux.  For now, I'm running Windows in VirtualBox for Skype for Business connectivity.  I do too many calls with it to dump it.   

Other than that, this platform is working really nicely.  I have a few little things to work around now, such as working around the Cisco VPN by using VDI, which only works if I run the VMware View client from a prompt (argh), but that's not too bad.   Mac users don't have it much better.

Ah, just remembered one more.  Garmin Connect.   I have an older model 310xt Garmin watch, and it connects with a damn ANT+ stick.  I can't seem to find a Garmin app for Linux, and I can't seem to get VirtualBox to see the stick when it's plugged in.  Fortunately, a fella wrote up an open source ANT tool that lets me just run a command it it pulls all the activities from the watch into individual FIT files, that I can then upload to Garmin.   I can still show off my runs.   

I'll give this 3 months and see how I feel.   So far, I'm good with it.