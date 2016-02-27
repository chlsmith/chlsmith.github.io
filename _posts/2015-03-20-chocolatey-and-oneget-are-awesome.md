---
layout: post
title: Chocolatey and OneGet are AWESOME
date: 2015-03-20 08:22
author: chlsmith
comments: true
categories: [Uncategorized]
---
There's a sweet application called Chocolatey (http://chocolatey.org) that allows you to run a single command to install other applications.   On the Chocolatey servers, they have tons of applications stored, such as Firefox, Chrome, Notepad++, and other awesome freebies.   You install the little Chocolatey application on your computer, then to install another program, you simply open a prompt and enter "choco install firefox", or whatever app you want to install.

I've written a simple little script to install all the applications that I need on my computer.   You can see it below.

-----------------------------------------------------------------------

<em>@powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" &amp;&amp; SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin</em>

<em>choco install notepadplusplus.install -y</em>
<em>choco install javaruntime -y</em>
<em>choco install googlechrome -y</em>
<em>choco install 7zip.install -y</em>
<em>choco install firefox -y</em>
<em>choco install vlc -y</em>
<em>choco install adobereader -y</em>
<em>choco install sysinternals -y</em>
<em>choco install putty -y </em>
<em>choco install filezilla -y</em>
<em>choco install fiddler -y</em>
<em>choco install adobeshockwaveplayer -y</em>
<em>choco install silverlight -y</em>
<em>choco install greenshot -y</em>
<em>choco install rsat -y</em>
<em>choco install git.install -y</em>
<em>choco install mssqlservermanagementstudio2014express -y</em>
<em>choco install visualstudiocommunity2013 -y</em>

----------------------------------------------------------------------------------------------------------------------

You can simply remove any of the lines for applications you don't want.  The first line actually installs the Chocolatey add-in, so you don't even need to install anything before running this.   I rebuilt my computer the other day and this came in super-handy, as I just ran this script and everything was done automatically.

Microsoft have built a similar tool (actually, damn near exactly the same) called OneGet (http://oneget.org).   It's so similar that you actually can connect to the Chocolatey storage to download and install applications using the OneGet toolset.   OneGet acts as a PowerShell add-in, so you have to be comfortable with PowerShell to use it.   You can download OneGet right now from the link above and start using it if you choose.   MS is going to include this in Windows 10.

This represents a GREAT STEP for Windows.   Linux users have run apt-get forever to install and update their applications.   This does the same thing.   All you ever need to do to update your program is run the Chocolatey or OneGet update.   FINALLY!!!!
