---
layout: post
title: Learn The Basics
categories: [work]
published: true
---

As mentioned in my previous post, it's time to talk about how to learn SQL, PowerShell, and Bash, which I think are the most foundational skills all infrastructure-types should know.  I'm not going to bombard this post with a bunch of links, because you can Google things yourself.   

I'm the type of learner who gets the most benefit from seeing someone do something, then doing it myself.   I'm not as good with books or just manuals, even though I can certainly get by with that kind of learning.   It's just longer.   I'm a firm believer in videos, such as those from CBT Nuggets or the Microsoft Virtual Academy (MVA), plus some little lab-type projects.   In most cases, if I've seen someone do the work, I don't even need the labs to reinforce it.

As mentioned in the previous post, I learned SQL through an actual instructor-led course from New Horizons.  It was great, but I could've done the same thing with a video series on YouTube.  I learned most of my PowerShell basics from an MVA course.  Bash is one that I'm self-taught on, but there are tons of online video tutorials.

Books are an obvious choice, too, plus you can get some nice "cookbooks" or examples to go back to later.   For the basiccs, you can even get older versions of the books and start from there.   The older versions are usually dirt cheap and can be picked up at Half Price Books or even the library, though you have to return the ones from the library.

Finally, the best way to learn these things is to DO THEM.  If you are fortunate enough to be on a helpdesk or be a junior admin somewhere, you can start today by simply using these tools for your current tasks.   

1. SQL:  Figure out a question that you need to answer that the software you use every day should be able to tell you.   Find the answer within the software, if it's available there.   Ask a DBA to give you a connection string and a READ ONLY account to the database, connect to it with Access, and start looking for the answer using regular SQL.  Use the query builder if you have to at first, but always go back to straight up SQL where you can.   Yes, you are likely to get a bunch of rolling eyes at the mention of using Access, but it's a tool that's probably already on your computer, so use it.   Build a few reports from the queries you've made, answering questions that you don't know how to figure out from your software app.   Show your boss.   Get a raise.

2. PowerShell:  Instead of using AD Users and Computers, Use the Active Directory module for PowerShell to add AD users.  Once you figure out the first one, just save the command and use it forever.  (Remember that that's a MAJOR advantage of using PowerShell in the first place.)  Instead of using RDP to get on a machine to find out how much RAM the thing has, use PowerShell with a remote CIM instance.  Most people who use PowerShell started off just using it as a shell to get tasks done, and then kinda "graduated" to scripting things out.   As a matter of fact, I still use it as a shell every day.   

3. Bash:  This is tough in a Windows shop, because you likely won't be using it every day.  Here's my tip: rebuild your computer with Linux and make it work.   For your Windoes work, if you have a remote desktop connection to a jumpbox on your network, simply use that for everything.  If you don't, install VirtualBox and build yourself a Windows VM on your Linux computer.   Use Linux as the primary OS for EVERYTHING that you can.  If you get Excel or Word documents, use the open source analogs for them, or use Office 365 if you have it.  If you can, use Google Docs or another cloud solution as your productivity suite.  Search for and use alternatives for everything you can.  Finally, once you have the apps you need, keep that shell open and use it instead of file explorer or whatever it's called in your Linux distrubution.   Use shell editors instead of Notepad for your own notes.  Just jump in with both feet.   

Hopefully these things make sense and someone can use these ideas.  These are certainly not Earth-shattering ideas, and anyone can start doing them today.   The main point is to get outside of your comfort zone, learn how to do things in different ways, and see how your productivity will improve.       
