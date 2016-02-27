---
layout: post
title: Network Security Groups
date: 2016-01-08 17:23


categories: [Uncategorized]
---
Two posts in a day?   Yes....because I'm afraid if I wait until Monday, I'll forget this stuff.

I've been working with Azure Network Security Groups (NSG) today.   For the uninitiated, imagine firewall rules that you can apply to subnets within your Azure network or to specific VMs.   NSG can basically replace all the ACLs on your VM endpoints, allow you to more fully control network traffic between your subnets, and can give you granular control on your VMs.   I envision replacing all of my endpoint ACLs and all of my Windows Firewall configuration with these, once I get them right.

What did I learn today?
<ol>
	<li>The moment you apply an NSG to a subnet, the endpoint ACLs on any VMs within the subnet are basically deemed useless.  If you have an endpoint ACL that restrict connections, as soon as you turn on the NSG, if you don't have the restriction configured, your connection is wide open to the Internet.</li>
	<li>Each rule is made up of a Name, Direction, Action, Source Address, Source Port, Destination Address, Destination Port, and Protocol.   This is like every other firewall rule I've ever put in.   One tip here, though, is that on Inbound rules, if you're wanting to open, say, port 443, you need to put that on the Destination Port.   Leave Source Port at "Any" or "*".    I was putting the ports in both parts, but it wouldn't let inbound connections work at all that way.</li>
	<li>The new Azure portal is pretty nice in that you can open a subnet, see all the VMs in the subnet, and then use that to browse into the endpoints.    Much easier than in the old portal, which I don't think could show you what VMs were on what subnets at all.</li>
	<li>Reiterated to me that you always do staging first.   I left off one endpoint from one NSG and I basically crippled SQL connections to a db server there.   Do your homework first and be careful.</li>
</ol>
These worked as advertised and I think it's going to be the right path for me.   I'm still trying to figure out how to do things on VM-level NSGs for stuff like "RPC Dynamic Ports" and ICMP, but at least I can do some network-level stuff now.    Pretty cool.

End goal will be to have the subnet NSG and some templated VM NSG in such a condition that I can just add a VM, assign it to the right subnet, give it a VM NSG, and never have to worry about Windows Firewall on the machine.  Hell, I could even disable Windows Firewall altogether if I'm lucky.   Good times.
