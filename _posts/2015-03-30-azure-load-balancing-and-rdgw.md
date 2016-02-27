---
layout: post
title: Azure Load Balancing and RDGW
date: 2015-03-30 13:45
author: chlsmith
comments: true
categories: [Uncategorized]
---
I'm trying to get Remote Desktop Gateway (RDGW) working on Windows 2012 with some load balancing provided by either Azure Load Balancing or Traffic Manager.   RDGW was easy enough to set up on a couple of machines and I was able to open endpoints individually to each, and then I verified that they worked.   When I enabled a load balanced endpoint, though, it was flaky.   Sometimes it worked and sometimes it didn't.   This isn't too surprising, because this whole thing may be unsupported anyway due to sticky session support.

Now I'm moving my two machines, built in the same cloud service, into their own.    After that, I'm enabling individual endpoints on them, then going to set up a traffic manager connection around them.   My understanding is that Traffic Manager is basically a DNS trick, so I'm hoping that with it, I can point computers to the traffic manager IP and it will round robin the connections.   More to come....
