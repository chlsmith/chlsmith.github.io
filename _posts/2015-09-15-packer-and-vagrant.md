---
layout: post
title: Packer and Vagrant
date: 2015-09-15 12:03
author: chlsmith
comments: true
categories: [Uncategorized]
---
I waslooking to find a way to make my Chef and DSC testing easier, so I asked Steve Murawski for some help.   His suggestion was to use test-kitchen, which I'd heard of, but never started messing with.   To get that working, though, on Windows, you have to have a way to get a machine that you can spin up to test against.   Steve pointed me to a great blog post on how to use the Packer tool with Vagrant and test-kitchen, so you can take care of your gold images and your test deployment.

http://bit.ly/1Kdpy08 &lt;- The important link

Now it was time to really jump into this and figure out what I can do.    Turns out that the Packer and Vagrant tools answer questions that I've long had, and they do some of the very things that I've tried to do forever.   In my past, I was the one who had to take care of VMware images and update them from time to time.   I have spent several hours of my life doing just that, spinning one up, updating it, and shutting it down.    Each time someone wanted something new included, I would do the same to add it.

This is where Packer comes in.  Packer provides a way to create a JSON file containing the configuration you want in the image, for both things that run during the deployment and scripts that are injected into the machine to run post-deployment.   Within the JSON file, you tell Packer what type of system to deploy on (VirtualBox, VMware, etc.), point it to your Windows ISO, fill in some other info, and run it.   The Packer tool then takes your config file, starts up a new VM in whatever platform you've chosen, builds it per your specification, and then shuts it down.   This leaves you with a VHD/VMDK file that you can put wherever you want.

To make it even more fancy, you can layer this on top of Vagrant.   Vagrant allows you to start and stop machines with just a single command, and it works with basically every platform (again, VirtualBox, VMware, etc.)  You don't really need Vagrant to use Packer, but you do need Vagrant to use test-kitchen.    Vagrant also hides most of the internals of the hypervisors, so you don't have to know how to do everything in the hypervisor to make things happen.  That's pretty nice, since you don't always want to do everything from a GUI.

Finally, I'm getting ready to start using test-kitchen, or even better, using dsc-kitchen.   I haven't done it yet, so more to come on that.

A few notes on what I had to do to get the Packer build to work right.

First, I used VirtualBox as my hypervisor on my machine, because that's the default with Vagrant and it's what was used in the step-by-step instructions from the link.   I've always liked VirtualBox better anyway, as it's always "just worked" for me.

Second, I downloaded and used a Windows 2012r2 ISO and changed the path in the JSON file to point directly to it.

Third, I had a lot of problems getting WinRM to work on the new VM.   It would come up and the port forwarding discussed in the link worked, but for some reason the actual Packer program would never connect to it.   After some digging with the logs, I found that it was looking for the wrong port.   I posted an issue regarding it into the Git project and got the response that I didn't need to forward WinRM, as is done in the example.   I took out the two lines for port forwarding for WinRM from my JSON file and, lo and behold, it worked immediately.  They are:

["modifyvm", "{{.Name}}", "--natpf1", "guestwinrm,tcp,127.0.0.1,59855,,5985"]

"winrm_port": "55985"

Turns out that the forwarding still happened automatically, which I find odd, but I didn't write it.   It works now.

Finally, logging in Packer is tricky.   You have to set a couple environment variables, of all things.   PACKER_LOG = 1 enables logging.   By default, it will put it right on your screen only.   To save to a file, you need to set PACKER_LOG_PATH = "c:\&lt;path&gt;\&lt;filename&gt;.log".    It's unusual to me to not be able to just pass those through parameters, but I don't see a way to do it.   I would TOTALLY SUGGEST enabling logging on Packer, or else when you run the scripts,you won't see squat.

Anyway, there you have it.   A couple more links for your enjoyment.

https://www.packer.io/   &lt;- Packer

https://www.vagrantup.com/   &lt;- Vagrant
