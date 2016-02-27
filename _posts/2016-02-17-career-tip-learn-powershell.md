---
layout: post
title: Career Tip: Learn PowerShell
date: 2016-02-17 10:07
author: chlsmith
comments: true
categories: [Uncategorized]
---
I don't remember if I've posted on this before or not, but it's worth repeating anyway.   If you are a systems administrator or engineer who works in the Windows environment, you need to learn PowerShell now.   Even if you are primarily a Linux guy, if you work in Windows AT ALL, you need to learn PowerShell.

PowerShell v5 is going to be released basically any day now.   v5 has all kinds of nice features in it, particularly in regards to Package Management.   Windows Server 2016 has a "Nano Server" installation option, which basically is a headless server that can only be managed remotely via PowerShell or other tools.  Windows Server Core, which has been an installation option since Windows 2008, has PowerShell built-in, so you can do anything you want to on those machines from within the shell.

Microsoft is NOT moving away from this direction any time soon.   Jeffrey Snover, the inventor of PowerShell, has recently been promoted to be Distinguished Engineer, architecting everything on the Windows Server and System Center products.   As such, you can expect that PowerShell will become even more ingrained into everything, and all of these products are going to be even more manageable with it.   There are PowerShell modules for Exchange, Active Directory, SQL Server, SCCM, you name it, so a little foundational learning will carry you a long way.

Learn it now.   If you don't, in 5 years, you're going to be playing catchup.  In 10 years, you may just be looking for another career.   The GUI on Windows Server is slowly dying, and I don't think Snover will have it any other way.   When you're finished learning PowerShell, don't forget that PowerShell Desired State Configuration (DSC) is available and right around the corner, too, and you're going to have to skill up on it.   The days of doing server management via RDP or console sessions are over.

Here's a couple readings and videos to get you started.   These are a little older now, but the concepts still apply.
<ul>
	<li><a href="https://mva.microsoft.com/en-US/training-courses/getting-started-with-powershell-30-jump-start-8276">PowerShell v3 Jump Start Class</a> - Taught by Snover himself.   It's a great start down this path.  I don't see one for v5, but I'm sure there will be one eventually.</li>
	<li><a href="http://www.jsnover.com/Docs/MonadManifesto.pdf">The Monad Manifesto</a> - Years ago, Snover published this as a guide to show the direction he thought things should go.   Over time, PowerShell has become what he was calling "Monad" initially.   A Must-Read.</li>
	<li><a href="https://blogs.msdn.microsoft.com/powershell/">The PowerShell Team Blog</a> - Great resource on what's coming down the pipeline.   If you're staying on top of this, you're staying on top of Windows Server, too.</li>
</ul>
&nbsp;
