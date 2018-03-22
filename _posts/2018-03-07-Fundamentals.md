---
layout: post
title: Fundamentals
categories: [tech]
published: true
---


One of the main tenets of the DevOps movement is that automation is key to replacing much of IT operations work.  Things like setting up new servers (particularly in the cloud but at least virtualized ones), doing health checks to make sure servers are configured as they should be, and deploying new software are all targets of this automation.  This automation takes work up front, but makes your servers easily replacable and "cattle", in that instead of worrying about babysitting them, you can just kill them and replace them at will.   Because, I guess people do that with cattle.

In my experience, I find you can only make a portion of the infrastructure "DevOps-y".  There are support systems that must remain in place really throughout the entire lifecycle of your other DevOpsed systems.  Some examples are Active Directory, DNS servers, management servers, jumpboxes, monitoring systems, and even some of the automation systems themselves.  These systems need to be reliable all the time, even while the DevOps-y systems are being killed and recreated.  Fundamentally, these systems should be treated much as they always have been.  They need to be backed up.  They need to be patched.  They need to have antivirus on them and that needs to be updated.  Their logs need to be examined from time to time.  Fundamental IT stuff.  Unsexy stuff.  

I have watched engineers spend a whole lot of time automating the deployment of these support systems.  Building Chef servers.  Spinning up AD controllers and scripting out the usernames that need to be in place for everything else to work.  Building Jenkins from the ground up with a bunch of scripts.  In every case, this has been a giant headache and a whole lot of guys have lost a whole lot of hair, and I just don't see the benefit.  

I LOVE the idea of "Infrastructure as Code" for all servers, including support systems.  For documentation and disaster recovery purposes, IaC is the second to none. This doesn't mean to me, though, that these support systems need to be completely coded.  Do the code to spin up a Windows 2xxx server, join the domain, put some necessary tools on there, harden the server from a security perspective.  Install the necessary major apps that the server needs to serve up.  Just remember that it is not useful to the company to replace these servers regularly.  Once the software is installed, log in and set it up manually inside the VM according to whatever documentation you have.  Update that documentation accordingly.   Then get that system on a backup solution so you never have to revert back to the base machine.  

For your servers that are used to host the software your company makes money from, the more you can automate the deployments to new servers every time, the better.  Focus your efforts to DevOps the shit out of those and get the bang for your automation buck.

