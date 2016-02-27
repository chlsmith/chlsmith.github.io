---
layout: post
title: Formatting Disks After Deployment
date: 2016-01-08 10:10


categories: [Uncategorized]
---
I don't usually post code snippets or whatever, but I think it's time for me to do so.   I have some sweet little ones here and there, and I might as well publish them this way so others can use them if they need them.

One of the first difficulties I had when deploying new VMs was formatting all the disks that I attached to the machine after it was deployed.   In Azure, the system disk always formats to be the C: drive, and there's always a D: drive attached for "temporary storage".    However, as I was automating my server builds, I didn't really have a way to format additional data disks that I attached.

Enter the Custom Script Extension.   This extension allows you to push a PowerShell script into a VM and have it just run.   It's pretty slick in that it runs locally, just as if you were logged into the machine, and it puts some nice logging under

<em>"C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension"</em>

so you can find out what happened during the execution.

In my deployment script, after the VM is built, I simply pass in the following script to format all the additional drives and assign them the next available drive letters.
<pre><em>----------------------------------------------</em>
<em>Function SetupDisks()</em>
<em>{</em>
<em> # This will initialize and format any uninitialized disks on the system and assign the next available drive letters to them</em>
 
<em> $diskstoformat = get-disk | where-object {$_.numberofpartitions -eq 0} | sort {$_.number}</em></pre>
<pre><em>Foreach($disk in $diskstoformat)</em>
<em> {</em>
<em> $disknum = $disk.number</em>
<em> $label = 'Data'+$disknum</em></pre>
<pre><em>$disk | Initialize-Disk -PartitionStyle MBR -ErrorAction SilentlyContinue</em></pre>
<em>new-partition -disknumber $disknum -usemaximumsize -assigndriveletter:$False </em>
<em> $part = get-partition -disknumber $disknum -number 1 </em>
<em> if($disknum -gt 1)</em>
<em> { </em>
<em> $part | Format-Volume -FileSystem NTFS -NewFileSystemLabel $label -AllocationUnitSize '65536' -Confirm:$false -Force</em>
<em> }</em>
<em> else</em>
<em> {</em>
<em> $part | Format-Volume -FileSystem NTFS -NewFileSystemLabel $label -Confirm:$false -Force</em>
<em> }</em>
<em> end</em>
<em> $part | Add-PartitionAccessPath -AssignDriveLetter</em>
<em> }</em>
<em>}</em>
---------------------------------------------
Taking a look at this, here's what's happening:
<ol>
	<li>First, I pull all the disks that have no partitions.</li>
	<li>For each one, I assign it a number and label, then initialize it.</li>
	<li>Next I create a single maximum-sized partition on the disk.</li>
	<li>If I'm on the first disk, I just format it with normal NTFS ....otherwise, I change the allocation size to 65536 to make better use of the disk.   (This isn't necessary generally, but I do it because only my SQL VMs have more than one data disk, and I use those to store my data, logs, and backups.    My "standard" VM has an attached data disk, which I don't use the allocation on.)</li>
	<li>Finally, I assign a drive letter.</li>
</ol>
This works every time.   What took me the longest was figuring out how to get the disks to initialize in a reliable way.   Once I got the initialization down, it was pretty straightforward.
