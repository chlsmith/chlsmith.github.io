---
layout: post
title: DSC Adventure
date: 2015-08-20 21:04


categories: [Uncategorized]
---
Man, this PowerShell DSC stuff is such a new way to do things.....for a guy coming into the industry, it has to be intimidating.  It is to me, and I've been at this for 15 years.  Basically, gone are the days where you can get into IT and just click Next a bunch of times, check some boxes, and move on.   Even systems that require a bit more skill, like Group Policy, are a breeze to use compared to DSC.

Here's why, and it's tough for an infrastructure guy: you have to have some level of skill doing development.   You don't have to be a full-on developer, but you better not be afraid to look at some code to troubleshoot things.   You better know how conditional statements, iterative loops, and probably even an idea of object-oriented programming, all work.    You can get by at first just by filling in some JSON files with property values and then applying them, but you're not going to get far without creating your own custom resources or customizing existing ones.

This could be because the technology is so new, but I'm not sure.   I don't know that the people working with it now want to make it any friendlier, and I don't know that anyone is making some sort of GUI-based solution to create or apply them.   There are some third party systems like Chef and Puppet that do some work with them, but those aren't the simplest things to pick up either.

As for my own progress, I'm getting there.   I've modified a couple of resources on my own and even created a pull request for my changes on one of them.  (I don't think it got pulled, but whatever.)   I'm not a programmer by training, so I knew this would be a step.   I think it's a good one, though.   The technology is slick, it's native to Windows, and it's far more powerful than anything else that is out there, including GPO.   The promise is that going forward it will become THE ONLY way to configure Windows servers.  I don't know if that will become totally true or not, but so far, Snover hasn't lied with putting the Monad Manifesto into place.

If you don't do DSC now, you'd better get into it soon.   If you don't even do PowerShell now, you are behind and need to get working on it.   I haven't really found classes on these things, as Microsoft is treating it as just something Windows people have to know.   It's not like every other technology that they create, then put out classes, exams, and certs in them.   With PowerShell and DSC, you just need to do it yourself.   The MVA courses are good and there are some decent videos out there you can create a learning plan out of.   Take a day, do a full course.   Spend the next week using it as much as you can in real life.   Take another day, do another full course.   Spend another week doing it.   Keep doing that, and within 3 months you should be damn good.   Where am I now?   On a scale of 1-10, I'd give myself an 8 in PowerShell and a 5 on DSC.   Relative to most admins I know, though, I'm a 10 on both....there just doesn't seem to be the jump to do this stuff out there, unfortunately.   I don't know why.

Well, I guess I do.   The learning curve is pretty steep.  But man, is it awesome once you get there.
