---
layout: post
title: Tons of Learning
date: 2015-07-28 16:14


categories: [Uncategorized]
---
The last couple of weeks have been a crash course on SQL Server in Azure IaaS.   We moved our North America Multistore database over to Azure and it wasn't the smoothest transition ever.   The old DB server was a small Windows 2003 server running SQL 2005.   Little server, little DB, never ran into any performance problems, etc.   Figured this would be a cake job and just move easily.

The server I put it on for testing was one of our standard server deployments, running SQL Server 2014 on Windows 2012 R2.   Got it set up, the DBA signed off on it, and QA did their tests and everything was a go.   We moved, and under real user load, it was so slow that queries in our app were timing out for all of our dealers on it.   Since we had gone from SQL2005 to 2014, we couldn't go back to the old server.   What now?

To keep the price down, we tried to add disks to the machine and stripe across them using Windows Storage Spaces.  This would provide more throughput to the disk, which was, without a doubt, our bottleneck.   This helped some, but we got too many VHD files in a single storage account, and Microsoft started throttling our storage throughput, killing our dealers' queries again.

I moved everything off of the storage account that I could, to get us under the 40 limit again, and waited another day.   Everything was okay, but we still got a few calls here and there...unacceptable.

Azure support told us that we had to move to Premium Storage, which is more expensive, but runs more like an on-premise server.   I built the server using their guidelines and we migrated.   Not a single problem since.

Lessons learned:

1. Don't try to save money initially, but build servers that will work and try to scale them back as much as you can afterward.   This would've saved a lot of headaches for our user base and still gotten us to the same final solution.

2. Perform load testing on both the current systems, such as perfmon logging, and on the systems you want to try to run on.   Don't just guess that you'll be okay because the current systems are old or slow or anything like that.   Use real data to make your case.

3. Don't just shrug off best practices because you've been doing things your way and things have been okay.   I did that here and, sure enough, got bitten big time.

Some docs for future reference:

SQL Server Best Practices on Azure:  https://msdn.microsoft.com/en-us/library/azure/dn133149.aspx

Performance Monitor on Windows:   http://www.handsonsqlserver.com/how-to-capture-the-performance-monitor-counters-and-objects-using-perfmon/

Azure Sizing Documentation:  https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-size-specs/
