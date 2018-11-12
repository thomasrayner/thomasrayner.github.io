---
layout: post
title: Detecting An Exchange Management Shell Connection
date: 2015-08-19 08:30
author: thmsrynr@outlook.com
comments: true
categories: [Exchange, exchange, microsoft, PowerShell, powershell, PowerShell ISE, powershell remoting]
---
You don't log onto an Exchange server via RDP and open the Exchange Management Shell application when you want to do Exchange-PowerShell things, do you? You follow the steps in my <a href="http://www.workingsysadmin.com/opening-a-remote-exchange-management-shell/" target="_blank">Opening A Remote Exchange Management Shell</a> post, right?

But how do you detect if if you have an open remote connection or not? Well there's a bunch of different ways so here's an easy one. First, though, we need to understand a couple things about what happens when you open a remote Exchange Management Shell connection.

Here's what the output of my <strong>Get-Module</strong> cmdlet looks like before I do anything Exchange-y.

[caption id="attachment_243" align="alignnone" width="1217"]<a href="http://www.workingsysadmin.com/wp-content/uploads/2015/06/6-5-2015-10-07-44-AM.png" target="_blank"><img class="wp-image-243 size-full" src="http://www.workingsysadmin.com/wp-content/uploads/2015/06/6-5-2015-10-07-44-AM.png" alt="Get-Module before anything Exchange related" width="1217" height="167" /></a> Get-Module before anything Exchange related (click for larger)[/caption]

I'm in ISE, I have the AD cmdlets added. Nothing going on here is too crazy. Now here's what it looks like after I open a remote Exchange Management Shell connection like I told you how to do in the post linked above.

[caption id="attachment_244" align="alignnone" width="1167"]<a href="http://www.workingsysadmin.com/wp-content/uploads/2015/06/6-5-2015-10-14-46-AM.png" target="_blank"><img class="wp-image-244 size-full" src="http://www.workingsysadmin.com/wp-content/uploads/2015/06/6-5-2015-10-14-46-AM.png" alt="Get-Module after adding Exchange Management Shell" width="1167" height="279" /></a> Get-Module after adding Exchange Management Shell (click for larger)[/caption]

Notice that the Exchange stuff gets added under a tmp name? And that it's different every time? That doesn't exactly make it easy to detect. With the ActiveDirectory cmdlets you can just run <strong>Get-Module -name ActiveDirectory</strong> and it will either return something or not. Easy. How are you supposed to do that in a predictable, repeatable fashion for Exchange, especially since any other <a href="http://www.workingsysadmin.com/quick-tip-opening-an-exchange-online-protection-shell/" target="_blank">remote shells created to other services</a> in the same manner may also be added with a <em>tmp_</em> prefix?

In order to figure out how we can determine if we have a module added that belongs to a remote Exchange Management Shell, let's take a closer look at the tmp module that just got added.

[caption id="attachment_245" align="alignnone" width="1158"]<a href="http://www.workingsysadmin.com/wp-content/uploads/2015/06/6-5-2015-10-19-22-AM.png" target="_blank"><img class="wp-image-245 size-full" src="http://www.workingsysadmin.com/wp-content/uploads/2015/06/6-5-2015-10-19-22-AM.png" alt="Details of the last module added" width="1158" height="208" /></a> Details of the last module added (click for larger)[/caption]

At first glance, we're obviously not going to be able to use the Name or Path attributes to identify remote Exchange Management Shell connections. ModuleType, Version, most of the others all look useless for us here. What looks useful, though, is the Description attribute which reads "Implicit remoting for http://my-exchange-server.fqdn/powershell". That, we can work with. Here's my code to tell me if I have a module added whose description is for a remote session to my Exchange server.

<pre class="lang:ps decode:true ">get-module | select Description | ? { $_ -match "my-exchange-server" }</pre>

The code will either return the description of the module if it's added, or null. You can work with it like this.

<pre class="lang:ps decode:true ">$ExchAdded = get-module | select Description | ? { $_ -match "my-exchange-server" }
if ($ExchAdded) { write-host "Yes, added" } else { write-host "No, not added" }</pre>

Check it out.

[caption id="attachment_246" align="alignnone" width="760"]<a href="http://www.workingsysadmin.com/wp-content/uploads/2015/06/6-5-2015-10-29-26-AM.png" target="_blank"><img class="wp-image-246 size-full" src="http://www.workingsysadmin.com/wp-content/uploads/2015/06/6-5-2015-10-29-26-AM.png" alt="Code at work" width="760" height="186" /></a> Code at work (click for larger)[/caption]
