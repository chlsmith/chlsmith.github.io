---
layout: post
title: Azure Security Center
date: 2015-12-17 13:24


categories: [Uncategorized]
---
Microsoft now has released to Public Preview the Azure Security Center service, and, man, am I impressed.    I love the potential in the product and am just dreamy-eyed at the products people use every day that this thing can replace.

Consider your most basic server scenario:  what a new company must have to operate.   First thing is probably a place to store files.   You probably need a print server, too (YUCK).   You probably need some way to secure the files and get some permissions on them, so if you're like most places, you'll need Active Directory.    You will certainly have Internet access and need antivirus and some software to manage that on your computers.   You probably need some updating software to keep all of the systems up-to-date.

In my most basic scenario, I envision about 5 servers:
<ol>
	<li>2 for Active Directory for redundancy</li>
	<li>1 for AV management</li>
	<li>1 for Update management (WSUS or the like)</li>
	<li>1 File/Print Server.</li>
</ol>
This isn't even including any servers that you may need for software that your company uses.   This is just the basics.  If you're small enough or don't have specific requirements for local servers, you can certainly do all of this through services like Google Docs or OneDrive, plus use Windows Update to take care of the rest.   In my world, though, those don't really cut it.   I have servers that I have to take care of, and those servers have "support server" requirements, even without a single user touching anything.

Here's where Security Center comes in.   It can now, and has the potential to, basically eliminate the AV and Updating systems.   It also will provide means to get at suggestions for solving security events, provide configuration recommendations for your servers all the time, and even can give you audit trails for things that aren't so easy to find in Windows alone.

Why is this such a big deal to me?   If you're on the fence about moving to IaaS, this added service should totally move you to the cloud side.  It's easy to operate, gives you a load of information, and can eliminate a lot of the worry you have day-to-day.

Now, I know nothing about AWS, but if you're considering what cloud vendor to go to, you need to look at this solution in Azure.   If Amazon doesn't have something similar, you might really want to consider going with Azure, particularly if you are going to have a lot of stable, rarely-changing VMs in our cloud.    If you are doing DevOps-type stuff only, you may not even care about this, but most of the IT departments I know still are building servers that need to stick around for a few years without worry.   For them, this is a killer app.

One thing I think is missing is backup monitoring.    Backup isn't always looked at as part of the security team's focus, but it sure seems to me like having secure, regular backups of your data is critical to the security of your company.   I would love for some backup monitoring and alerting to be integrated into this solution.    If that was to happen, I don't know that I'd have to look at any other portal on a daily basis to check on things.   "One Stop Shopping", as an old boss of mine used to say.
