---
layout: post
title: "Minor PowerShell DSC Fail"
published: true

categories: [Chef, Powershell, Technical, Technical]
---
(Notice I didn't say "fail"?  Fail is a freakin' verb.)

I'm starting to try out PowerShell DSC so I can integrate some built-in Microsoft goodness into my Chef recipes.   Chef is pushing this as a great solution, because it gets them out of writing their own recipes for everything, plus Microsoft promises to keep the DSC portions in the OS forever, as it's native.   This is a great idea, and I think it's very workable together.

We are now on Wave 10 of the DSC Resource Kits, and this newest "wave" contains all kinds of nice modules.   At this point, you can basically configure everything on a Windows box using DSC.   Pretty neat, and not so hard to do when you can integrate it with something like Chef to push out the configurations.

In the xNetwork module, there is a module called xFirewall that allows you to build firewall rules in Windows firewall.   Simple enough.    Firewall rules, regardless of the vendor, have always required basically 5 configuration items:

1.  The name of your rule.
2.  The source address or range of addresses.
3.  The destination address or range of addresses.
4.  The port.
5.  The direction of the rule (inbound or outbound).

Off the top of my head, I can think of nothing more important than those 5 items.   Here's where the xFirewall module fails.   You can easily create rules for the firewall, including Windows Firewall specific things like the application you're allowing, the "profile" you're putting it in, etc.   However, YOU CANNOT DECLARE THE SOURCE ADDRESS FOR THE RULE!!!!!

Looking through the DSC code, they are depending upon the "set-netfirewallrule" and "get-netfirewallrule" cmdlets to do the heavy lifting.   Set-netfirewallrule does have an option (-remoteaddress) that lets you declare the source address for the rule.   The get-netfirewallrule, though, doesn't pull this property into the results!!!   Therefore, you could feasibly set it, but within DSC, they couldn't do their test to see if the rule is the same as what you want to change!   Instead of fixing the get-netfirewallrule cmdlet and distributing a new version, they just left that little option out of the module.

That stinks.   I can certainly fix this on my own.  I totally see how to do it, but how much effort should I have to put into this thing?   I've posted on the Wave 10 download page to see if anyone can work on it.   Until then, I'll just use the Chef windows_firewall cookbook that I've already made work.
