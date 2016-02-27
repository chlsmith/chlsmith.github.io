---
layout: post
title: Azure VM DSC Extension
date: 2015-08-26 08:39
author: chlsmith
comments: true
categories: [Uncategorized]
---
What a discovery!   I've been trying for weeks to get an automated SQL Server deployment working in Azure, and every time I've gotten close, but never exactly where I wanted.

I started with doing a Chef recipe for the installation.  This worked, but I have problems getting the gems to install correctly in my Azure VMs.   After some work with both the Chef and the MS support teams, it appears that I have a problem connecting to rubygems.org to obtain the gems.   The main one I need is rubyzip, as I need to pull down and extract some files.   With my DNS setup, though, it doesn't want to work.   Seems like the rubygems.org site is kicking me back because of a new ".azure" top-level domain.   Kinda weird.

I then started messing with DSC.   Using the xSQLps module, I was able to install SQL Server using a push configuration pretty easily.   This was awesome, so I took that configuration and added it to a Chef recipe, as I don't have a DSC pull server available and don't really want one.   Chef has two methods to run DSC configurations:  dsc_script and dsc_resource.   dsc_script is kind of the "old" way, as it just runs the script on the machine, creates the MOF, and applies it.  That should've worked, but i couldn't figure out how to pass a credential in an encrypted fashion.  dsc_resource is the "new" way, but I've been asked to hold off on using it due to needing WMF5 and some more support hashed out.   After another call with Chef, I got dsc_script working, but then I was back to my original problem, needing to download the rubyzip gem first.   Argh....

Finally, I found the Azure VM DSC Extension, which allows you, via PowerShell, inject DSC configurations to run on an Azure VM one time.   Essentially, you publish a configuration to a blob storage location and then issue a "Set-AzureVMDSCExtension" command against the VM.    This causes the vm to pull the config and run it locally, regardless of if the LCM is set to Push, Pull, or Disabled.   Could this be the key?

I created a general script, as shown below, to download the Windows SXS folder to the machines.   This is already on most machines, but there are parts missing in Azure VMs that are needed later, so previously, I had just zipped the whole thing up and put it in a blob.  (I've changed a couple server names in the blob....insert your own.

--------------------------------------------------------------------

configuration GeneralConfig
{
import-dscresource -module 'PSDesiredStateConfiguration'
import-dscresource -module 'xPSDesiredStateConfiguration'

node ("localhost")
{
File Sources
{
Type = "Directory"
Ensure = "Present"
DestinationPath = "C:\Sources"
}

# downloads SXS Folder
xRemoteFile DownloadSXS
{
DestinationPath = "C:\sources\sxs.zip"
Uri = "https://<strong>&lt;storageaccount&gt;</strong>.blob.core.windows.net/<strong>&lt;container&gt;/sxs.zip</strong>"
}

# Extracts sources
Archive ExtractSXS
{
Ensure = "Present"  # You can also set Ensure to "Absent"
Path = "c:\sources\sxs.zip"
Destination = "c:\sources"
}

}

__________________________________________________________________________\

This script creates the c:\sources folder, downloads the zip to it, then extracts it.   Simple enough.

Next, you have to publish this DSC config into your blob storage.   You do this with the Publish-AzureVMDSCConfiguration cmdlet.  A couple of caveats here.   It defaults to publish it to whatever your current storage account is configured as in your subscription and it puts it in a container called windows-powershell-dsc.   You can change both with arguments to the cmdlet, and I suggest you do so so you can use the same files regardless of what your "current storage context" is later.

Once published, applying this to a machine, even an existing one, is pretty straightforward.   The following PowerShell does it.

Set-AzureVMDscExtension -ConfigurationArchive &lt;zip file created in publish process&gt; -ConfigurationName "GeneralConfig" -vm $vm -storagecontext $ctx | update-azurevm

$vm has to be a VM object that you get with "get-azurevm".

On the machine, there will be a log folder under c:\windowsazure\logs\plugins\Microsoft.Powershell.dsc\&lt;version&gt; that will contain a "DSCExtensionHandler" file.   This will show you to outcome of the run.   To get things working the first time, you may need to apply your config multiple times until you get a successful run, but once it works, you're ready.

Finally, in my build script, I just added a line at the end with the Set-AzureVMDSCExtension cmdlet from above.   As soon as the machine is deployed, the config is now injected and applied.

No longer do I need to try to do things with extra tools (Chef, pull server, whatever).  Now that I have it right, it will deploy the exact same every time via my script.   I can actually remove all of the Chef recipes I have to deploy the apps that I'm deploying in my "General" config, and drop all of them that deploy SQL.    Even if something gets broken down the road, redeploying is a breeze with this in place.

There you have it.   Hope this helps someone else.   My next step is to inject a custom script, or maybe even just add to the current one, to configure the SQL Server itself (default db location, log location, etc.)   That should be fun, but in the worst case, I can push that with a sqlcmd script using Chef for whatever.   Nothing to it.   :)
