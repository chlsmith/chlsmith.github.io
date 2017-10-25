---
layout: post
title: Imaging a Computer
categories: [tech,opinion]
published: true
---

Something I've probably ranted about before, but I'm doing it again.  One thing that every IT department I've ever been around has done is manage PC "images".   These images are usually built one time manually, and approved software is installed on them, maybe some registry hacks are done, files can be added/removed, etc.   Then, when a new computer is brought in, the team "images" the new computer by putting an exact copy of the first one on it.

I HATE THIS PRACTICE.   

1. There really is no such thing as an "image".  It's really just a bunch of files from the source computer.   The word just annoys me.

2. There are often errors on the source computer that the helpdesk ends up having to fix everywhere.  

3. The process becomes a crutch for fixing issues.   When a computer has a problem, a "bad image" is too often blamed, and the helpdesk will re-image the whole thing.  This is total cop-out.  The problem itself should get fixed and documented for later...not re-applying the same garbage as the first time.  This also creates a risk of losing the user's data during the process, which should be the number one thing the technicians worry about.

4. It's time consuming.  With every new batch of computers brought in, the team has to dedicate basically a whole person to nothing but imaging the new machines.  This can easily take a month in most organizations, and then the team spends several more months swapping the machines for the users, and then probably another month "re-imaging" the ones they have brought back.   It's a nightmare.

5. Every model of every machine must have an image, and these need to be updated regularly.  This is another several weeks of work per year for the team.

6. This process holds back OS upgrades to the entire organization.

What's the better way to accomplish deployments?  

1. Let the manufacturer install Windows for you.   The computers come in with Windows on them.   Use it.   Stop buying an enterprise license when you have it on the laptops when they show up.

2. Use a system like SCCM or similar to deploy the software you need.  It does take time, but you can easily control the apps that get deployed this way.

3. Use [Chocolatey](https://chocolatey.org/) to help.  A simple script can be written that will pull down and install all the software you probably need.  

4. Use in-place upgrades.  Too often, organizations are waiting for the IT team to get their "approved image" ready before deploying a new operating system.  Once it is ready, they then either need to upgrade when computers are replaced, or they have to go station-by-station to apply the new image.  Forget that crap....do in-place upgrades.   This isn't 1995.  In-place upgrades work now.  Microsoft has a ton of employees, and they rolled out Windows 10 this way.  [Proof](https://msdn.microsoft.com/en-us/library/mt637100.aspx) You  can, too.

5. When a PC is being replaced, either do it side-by-side at the user's desk or set their expectation that they will be down for several hours.  This sucks, but such is life.  They would deal with it for a new cell phone....they can deal with it for a new PC, too.  