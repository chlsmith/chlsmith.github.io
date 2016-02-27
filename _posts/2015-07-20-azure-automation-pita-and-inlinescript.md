---
layout: post
title: Azure Automation PITA and InlineScript{}
date: 2015-07-20 12:36
author: chlsmith
comments: true
categories: [Uncategorized]
---
I have found Azure Automation Runbooks to be a total pain in the ass.   First, I do all of my script work in a text editor or in the Powershell ISE, yet for some reason, I have to use MS's silly Azure Runbook tool to publish things.   Second, I've always had issues getting the runbooks to work right, because I've always just tried to copy and paste from PowerShell into the Workflow.

I finally found a solution to the second part today.   It's the InlineScript{} command.   Evidently, the workflows don't run in your normal PowerShell context, so you can use InlineScript{} to force specific commands to run in the "normal" way.   Well, forget that.   I just put my whole script into the brackets for InlineScript{} and it worked flawlessly.

What a silly way to do things.   Maybe it won't always work for some technical reason, but it worked this time.
