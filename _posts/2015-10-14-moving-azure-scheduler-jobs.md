---
layout: post
title: Moving Azure Scheduler Jobs
date: 2015-10-14 11:36
author: chlsmith
comments: true
categories: [Uncategorized]
---
Due to some poor prior planning, my company has a bunch of different Azure subscriptions used for different things, and billing is kinda tough.  Months ago, we chose to merge those subscriptions into just two:  one for real stuff that we want to administer and maintain, and another for folks to use for PoCs and so on.

After moving the VMs in IaaS to the new subscription, I now get to move the table storage, queues, scheduler jobs, and the other PaaS systems to the new subscription.   I have decided to start with the queues and Scheduler Jobs, which kind of go together, since the jobs are write to queue storage.

Problem is, I can't find a way to migrate the jobs anywhere.  The cmdlet "Get-AzureSchedulerJob" retrieves all of the settings for the jobs there, but not the messages that the jobs write.  The solution is to figure out how to get this using the REST API.

Using the hard work from <a href="https://open.bekk.no/windows-azure-scheduler-part-3-manage-using-powershell," target="_blank">this guy</a>, I was able to piece together a script that would download the current job definitions using the REST API.  The following two functions create the HTTPClient that is needed to get into a subscription and get the scheduler jobs from the given job collection.

<hr />

<em># this function gets the azure management certificate for the given subscription and returns the full httpClient connection</em>
<em>function get-azuremanagementhttpclient($xMsVersionHeader='2013-08-01', $sub) {</em>
<em> $cert = Get-AzureSubscription -SubscriptionName $sub -ExtendedDetails | select -ExpandProperty Certificate </em>
<em> add-type -AssemblyName System.Net.Http </em>
<em> add-type -AssemblyName System.Net.Http.WebRequest </em>
<em> $handler = New-Object System.Net.Http.WebRequestHandler </em>
<em> $handler.ClientCertificates.Add($cert) | out-null </em>
<em> $httpClient = new-object System.Net.Http.HttpClient($handler) </em>
<em> $httpClient.DefaultRequestHeaders.Add('x-ms-version', $xMsVersionHeader) </em>
<em> $mediaType = new-object System.Net.Http.Headers.MediaTypeWithQualityHeaderValue('application/xml') </em>
<em> $httpClient.DefaultRequestHeaders.Accept.Add($mediaType) </em>
<em> $httpClient</em>
<em>}</em>

<em># this function gets the jobs from the httpClient at the srcURI</em>
<em>function get-jobs($httpClient,$Uri)</em>
<em>{</em>
<em> $task = $httpClient.GetAsync($Uri) </em>
<em> $task.Wait() </em>
<em> if($task.Result.IsSuccessStatusCode -eq "True")</em>
<em> {</em>
<em> $jobs = $task.Result.Content.ReadAsStringAsync().Result # $srcSched becomes the JSON definition of the source jobs</em>
<em> } else {</em>
<em> $errorInfo = $task.Result.Content.ReadAsStringAsync().Result</em>
<em> $errorStatus = $task.Result.StatusCode</em>
<em> Write-Error "Call to GET $Uri failed with HTTP code $errorStatus and message $errorInfo"</em>
<em> }</em>
<em> return $jobs</em>
<em>}</em>

<hr />

Now that I have the jobs defined in text, I replaced the old storage account and queue names with the ones for my target location.   Finally, I used "ConvertFrom-JSON" to convert the $jobs output to a PowerShell object, and used New-AzureSchedulerStorageQueueJob to create the new jobs.

<hr />

<em>New-AzureSchedulerStorageQueueJob -Location $destLocation -JobCollectionName $destJobCollectionName -JobName $obj.id -StorageQueueAccount $destStorageAccountName `</em>
<em> -StorageQueueName $destStorageAccountName -SASToken $obj.Action.QueueMessage.sasToken -StorageQueueMessage $obj.Action.QueueMessage.Message `</em>
<em> -Interval $obj.recurrence.interval -Frequency $freq -JobState Enabled</em>

<hr />

This wasn't as pretty as I wanted it to be and it took a lot longer than it would have if "
Get-AzureSchedulerStorageQueueJob" had simply given me the message to begin with.   Oh well....works now.

As a to-do, I have to still manually change the Start Times on the new jobs, as they just go into the system with the current time as the start.   If you want to run something daily or weekly, though, you probably want to configure the times.    You can automate this with the Set-AzureSchedulerStorageQueueJob cmdlet or you can just do it in the portal.
