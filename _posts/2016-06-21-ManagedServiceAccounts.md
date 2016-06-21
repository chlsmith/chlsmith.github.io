---
layout: post
title: Managed Service Accounts Stink
categories: [work]
published: true
---

With Windows 2008, Microsoft debuted a pretty cool new user account type: the Managed Service Account.  "Service Accounts" are user accounts that are used to run something that requires no user interaction.  For instance, you may have an application service that has to run all the time on your computer, but you don't want to have to start it up yourself and have it running on a window.  

There are several security issues with these:

1. The passwords are shared.   You have to keep a central list of their passwords, so if the engineer who set it up is hit by a bus, the other engineers know how to troubleshoot the account.  
2. They are usually configured to have passwords never expire.  This is so you don't have things just quit working one day out-of-the-blue.
3. They often have some elevated permissions on servers.   If any of the passwords get hacked, the hacker has a lot more permission than you'd want.

These new "Managed Service Accounts"(MSA) were meant to address these issues.   You never configure the password for an MSA, and it changes automatically every so often.  The passwords are guaranteed to be complex, too, which is pretty cool.  

So far, so good.   Why do they stink????

1. They only work on the local machine and you cannot access network resources with it.   Blech.
2. If you get an error regarding the password, you can't troubleshoot it.   You can't verify that the password is right, nor can you reset it to something you know works.  This has happened to me with IIS, so it's a real concern.
3. The documentation on these things is slim.   Microsoft has some articles on them, but there aren't many 3rd party documents on it.   I think this is because they aren't widely used.

That's all just too bad.  The MSA is a great idea, but they really need some work to be useful.   
