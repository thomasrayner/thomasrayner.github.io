---
layout: post
title: Find Users Who Are Allowed To Have No Password Using PowerShell
date: 2017-03-22 08:30
author: thmsrynr@outlook.com
comments: true
categories: [active directory, active directory, activedirectory, password not required, passwords, PowerShell, powershell, user account control, useraccountcontrol]
---
You can use the UserAccountControl property of an Active Directory user object to enable and disable all kinds of neat functionality: <a href="https://support.microsoft.com/en-ca/kb/305144" target="_blank">https://support.microsoft.com/en-ca/kb/305144</a>. One of the things you can enable is for a user to have no password (bit in the 32 position).

While this only impacts users who connect to the console, and it doesn't mean that a user doesn't have a password (just that they might), it's pretty bad to leave that enabled for any users you've got.

Here's an easy one-liner to get a list of users with this problem.

<!--more-->

```
get-aduser -filter "useraccountcontrol -band 32" -properties useraccountcontrol\n```

This shows you all the users in your domain whose password not required flag is set.

Here's an easy way to fix it indiscriminately! Pipe the last command into...

```
 | foreach-object { Set-ADAccountControl $_.samaccountname -PasswordNotRequired $false }\n```

&nbsp;
