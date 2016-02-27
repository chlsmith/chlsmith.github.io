---
layout: post
title: RDGW with Traffic Manager is working!
date: 2015-03-31 08:15


categories: [Uncategorized]
---
Looks like I have RDGW load balancing working now.   I simply had to create two separate VMs on their own cloud services, then enable endpoints on each for ports 80 and 443.   This essentially provides two endpoints that I can use individually, if I want to.   I then set up a Traffic Manager for these endpoints and configured it for round robin load balancing.

What happens with Traffic Manager is a simply DNS trick.   Since each endpoint has it's own URL (&lt;service1&gt;.cloudapp.net and &lt;service2&gt;.cloudapp.net), and they are each open on the same ports, when a request is made to Traffic Manager (&lt;manager_name&gt;.trafficmanager.net), it simply responds with whichever URL it wants you to go to, then your client goes there.   Traffic Manager will verify that the endpoint is online, so it provides a level of redundancy, and can load balance based on different rules, but I used round robin since that's the simplest.

So far so good.   If it breaks, I guess it's back to the drawing board, but this is a pretty simple answer that I think should work for good.
