---
layout: post
title: FTP as a Service
date: 2015-12-30 09:13
author: chlsmith
comments: true
categories: [Uncategorized]
---
How can FTP as a Service be so hard to find and so damn expensive when I find it?   All I need is a cloud-based storage solution that support FTP with SSL encryption.   This should be so simple for Microsoft to offer in Azure, but, alas, they don't.

BrickFTP is a solution that appears, on the surface, to do everything I need it to do.   It's also inexpensive, which is awesome.   The problem is, unless you go with the highest price offering, all the usernames have to be globally unique within their entire system.   So two clients can't have a "CSMITH".

C'mon guys....make it so the usernames only need to be unique within the customer's individual account.   This shouldn't be that tough to manage from your end.   In your own database, just use a composite key with the customer account number and name as your "username" within your stuff.   Don't make your customers do some first-come-first-served thing with them.   Otherwise, the service is awesome.   It's easy to setup and works.     I don't want this one limitation to be a show-stopper, but at the moment, I'm afraid is.

Other FTP services are out there, but they are all pretty pricey.   Most of them are billed based upon the number of user accounts, too.   This makes sense, as I think they are seeing themselves as a kind of Dropbox replacement.    This isn't the model I'm working in, though, as I have just a few accounts that all need managed access to the same set of files.

Argh.  More research or keep doing it myself.

&nbsp;
