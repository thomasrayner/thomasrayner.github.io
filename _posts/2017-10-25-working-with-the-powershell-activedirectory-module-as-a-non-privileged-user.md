---
layout: post
title: Working With The PowerShell ActiveDirectory Module As A Non-Privileged User
date: 2017-10-25 07:00
author: thmsrynr@outlook.com
comments: true
categories: [active directory, active directory, activedirectory, PowerShell, powershell, PSDefaultParameterValues]
---
As a best practice, as an administrator you should have separate accounts for your normal activities (emails, IM, normal stuff) and your administrative activities (resetting passwords, creating new mailboxes, etc.). It's obviously best not to log into your normal workstation as your administrative user. You're also absolutely not supposed to remote desktop into a domain controller (or another server) just to launch a PowerShell console, import the ActiveDirectory module, and run your commands. Here's  better way.

<!--more-->

We're going to leverage the $PSDefaultParameterValues built-in variable which allows you to specify default values for cmdlets every time you run them.

First, set up a variable to hold your credentials.

```
PS&gt; $acred = Get-Credential -Message 'Admin creds'
```

Now, import the ActiveDirectory module.

```
PS&gt; Import-Module ActiveDirectory
```

And finally, a little something special.

```
PS&gt; $PSDefaultParameterValues += @{ 'activedirectory:\*:Credential' = $acred }
```

I'm adding a value to my $PSDefaultParameterValues variable. What I'm saying is for all the cmdlets in the ActiveDirectory module, set the -Credential parameter equal to the $acred variable that I set first.

Now when I run any commands using the ActiveDirectory module, they'll run the the administrative credentials I supplied, instead of the credentials I'm logged into the computer with.
