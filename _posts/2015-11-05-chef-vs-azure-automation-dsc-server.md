---
layout: post
title: Why I still use Chef.
date: 2015-11-05 10:08
author: chlsmith
comments: true
categories: [Uncategorized]
---
Chef has been a pretty good tool for me to use to configure computers in Azure.  I use Hosted Chef, which keeps me from having to run anything inside my environment other than the Chef clients on my computers.   I have some standard recipes and roles that I apply to my machines.

It took considerable effort me to get these where I have them now, which is basically at a stable, hands-off state.   I have some general recipes for Windows Firewall rules, some for software deployments, some for configuring Windows Updates, and so on.    I have then grouped these recipes into a bit of a hierarchy, where I have the "standard" role filled with recipes I apply to everything, and other roles built on top of that.   Maybe a SQL Server role that is made up of the standard role + a few more recipes.   Stuff like that.

When I need to change a firewall rule that is applied to everything, then, I simply change the single firewall recipe that is part of the standard role, and then, once everything checks in, it's rolled out.   Easy peasy.

DSC has offered me a new way to create my recipes, as opposed to the Ruby that Chef uses.   Since DSC is built into Windows, I can basically guarantee that it will be around for a long time.   The old Chef resources were built basically on command line tools that can change whenever Windows changes, and in some cases the command tools are limited as to what they can do, which then limits the Chef resources.   DSC gets around that by letting me do whatever I want, period.

There's always been a Microsoft-supported "DSC Pull Server" that lets you configure something like a Chef server with only native Microsoft stuff, but it's been kinda hokey.  For instance, to group computers together, you have to use some strange GUID thing.   To do composite configs, where multiple configuration files are used for a single node, it's always seemed bulky and ugly to me.

Microsoft has now released, at least in public preview, their Azure Automation DSC Pull Server, which can take the place of an MS DSC pull server.   Now, all in the cloud, you simply upload your DSC configurations, all the modules you use, and so on, and then configure your machines to check there to run the configs.    Sounds great, and it definitely has come potential.

I just tried it and I've found limitations already.   The main one, which is big, is that you cannot use composite configurations on this new system.   This means, basically, that for each "type" of computer you want, you have to have a separate, complete configuration.   For instance, you may have a "Standard" config that you put on your normal nodes, but then a full SQL Server config for your SQL servers.   Anything, however, that you want from the standard in the SQL one will need to be copy/pasted into it.   If you have 5 different SQL server types, even with just minor changes between them, that's 5 configuration files.   If you then want to change just a single item on them all, you have to update every configuration.   That can lead to errors down the road and just is unmanageable.

Sometimes I feel that Chef isn't giving me anything.   I just have it sitting there running, I'm using mostly DSC recipes for all of my work, and there is a free DSC pull server that I could roll out if I wanted.  However, Chef does allow me to just take generic configs, stack them up, and apply them to my nodes.  This flexibility is a killer feature to me.   I do not need to keep things filed away based upon the computers themselves, but by roles that I want computers to be.  Similarly, adding new computers with the same features is simpler, because I just say, "Hey, you're a SQL Server", and it becomes a SQL Server.

Maybe MS will do some improvements to make things better, but at least for now, Chef is still required for me.  Frankly, if the Azure DSC server remains the same as their regular DSC pull server, I don't foresee Chef going away anytime soon in my environment.  Another thing is that DSC is from the Windows Server team, not from their System Center team.   I think there are some boundaries that the server team cannot cross when it comes to creating management solutions for their systems.   If they created a full-blown Chef-type server, they would step on the toes of the System Center team, not to mention the fact that the Active Directory team has had Group Policy doing similar stuff for 15 years.
