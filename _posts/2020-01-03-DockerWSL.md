---
layout: post
title: Docker on WSL
categories: [tech]
published: true
---

I just setup possibly the strangest thing I've ever set up on my computer: Docker Desktop with Windows 10 WSL integration.  Thoughts of something like this a decade ago were just a hoop dream. I have Windows 10 with the latest insider build.  I setup Windows Subsystem for Linux (WSL) version 2 on it. I then installed Docker Desktop Edge release, which has WSL integration support. 

With those installed, I can actually run Linux containers, such as SQL Server for Linux, on my Windows laptop, without any kind of hyper-v virtual machine. It just runs inside of the WSL instance. 

### Setup Windows
The first thing you need to make this happen is Windows 10 version 18917 or higher.  I got what I needed by just joining the Fast Ring Insider group to always stay on the most recent release.  It's not necessary to take my bold step to do this, but I enjoy getting the new stuff, even if it's occasionally buggy.

Then you need to setup WSL 2 according to the instructions on Microsoft's [documentation](https://docs.microsoft.com/en-us/windows/wsl/wsl2-install). There are some technical steps required in PowerShell to make it work, but if you're considering WSL2, you can handle a little PowerShell in your life.

### Setup Docker Desktop

You should really use the edge release of Docker Desktop for Windows to make this work. Again, I'm not sure if it's "required", but it worked for me, so do it.  You can grab all the instructions and the download [here](https://docs.docker.com/docker-for-windows/edge-release-notes/).

Once installed, go into the settings and enable WSL 2 Integration. The service will restart when enabled. The really nice thing is that once it's done, you can go into Hyper-V Manager and you won't see a VM there for Docker Desktop.  That's because Docker is actually running everything within the WSL instance on the machine.

### What Containers To Run

There are two options for the configuration of Docker Desktop: enabled for Windows containers or enabled for Linux containers. If you are configured for Linux containers, you can only run Linux containers on Docker. If you are configured for Windows containers, you can run BOTH WINDOWS AND LINUX CONTAINERS!!

Why do Linux containers work when Docker is configured for Windows?  Because Windows will use WSL to run Linux containers in the background, and you just won't see it. 

This is a truly amazing feature of Windows 10. Not only can you run both OS-based containers, but they can interact with one another and everything just works. 

THAT SAID...If you are configured to support Windows containers, there are limitations on the Linux containers. One I found right away was that SQL Server for Linux images will not run. This is because SQL Server for Linux is not supported on WSL. That means if you don't use Docker and just try to install SQL Server for Linux within a WSL instance, it won't work.  

For me, SQL Server is critical. Therefore, I had to enable Docker to run Linux containers. They still all run within WSL behind the scenes, but SQL Server isn't smart enough to realize it. 

### Another Configuration Option

Since I'm configured to run Linux containers and I have Ubuntu installed within WSL, I can actually enable the Ubuntu instance to work with Docker. It's just a check box in the Docker settings to allow it.  

With this enabled, I can run PowerShell locally or bash within my Ubuntu WSL system, and BOTH OF THEM CONNECT TO THE SAME DOCKER INSTANCE.  I can then do all my Docker work from either place.  

This is really a cool feature, because if I want to be a Linux nerd, I can just do everything from there.  Even VS Code works from WSL, so I can do that, too. Total cross-platform integration for everything. Very cool.

### Conclusion

This is the coolest thing I've done in Windows ever. I do like having Ubuntu and Windows able to access the same Docker instance, even if I cannot, at the moment, run Windows containers.  Fortunately, I don't have any call for Windows containers anyway, so this works for me.  If I did, I could probably still do some hackery to make ti all work, but there's just no need.

Dump your Macs, dump your Linux VMs, and just use Windows 10 with WSL and Docker.  Everything is there. What a cool time to live.