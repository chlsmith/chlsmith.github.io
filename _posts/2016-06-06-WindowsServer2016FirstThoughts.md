---
layout: post
title: Windows Server 2016 First Thoughts
categories: [work, windows]
published: true
---

I just finished reading the new "Introducing Windows Server 2016 Technical Preview" book, and while I haven't really played with Win2016 much, the book has made me think of a few things.

1. If the content of the book is any indication, Microsoft is pushing very hard to make Windows Server THE virtualization platform of choice.  I don't know how Hyper-V on 2016 benchmarks against VMware, but it's clear that Microsoft is trying very hard.

2. The new storage features are pretty cool.   I really like that we can start pooling storage across nodes.   This looks awfully similar to what the folks at Nutanix are doing...

3. As a cloud-based Windows user, who doesn't have to deal with any kind of hypervisor stuff, storage networking, or even that much networking, what does 2016 really get me?  There's no meat in the book for things like Active Directory or RDS.  There was a small section on Multipoint Server, which isn't something I'm going to use.  If I'm not going to move to Nanoserver soon, is there any real reason for me to upgrade to 2016 from 2012R2?

4. I'm glad I got into IT when I did.  Maybe it's just me, but Windows Server 2016 is soooooooo much more complex than any previous version.  Many of the features for storage, compute, and networking virtualization look like they could be completely separate products.  I like that MS is pulling them down as roles in Windows Server, but it sure makes for a complicated learning curve for newbies.  

5. Microsoft is absolutely taking their learnings from Azure and pulling them down into Windows Server.  It's clear that technologies they've developed for their own Azure datacenters are being turned into standard roles.   This is really exciting and cool.   It almost feels like when an auto manufacturer builds standard features in their sedans that were first proven on the Formula One circuit.

6. Learn PowerShell now.  You won't be able to manage this new stuff without it.

7. Container service looks nice.  It appears that I can spin up a Server Core container and run anything on it, on top of a Nanoserver base.  I don't know how changes within the containers get committed to the images, so I'm not sure I can use them for things like AD controllers, but I'm sure something's coming down the pipe to make it happen.  

I guess now it's time to stand it up and start playing.  