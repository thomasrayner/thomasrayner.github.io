---
layout: post
title: Beginner PowerShell Tip - Using Variable Properties In Strings
date: 2017-11-29 07:00
author: thmsrynr@outlook.com
comments: true
categories: [active directory, beginner series, beginner series, PowerShell, powershell, string manipulation, string manipulation, strings]
---
If you're just getting started in PowerShell, it's possible that you haven't bumped into this specific issue yet. Say you've got a variable named <em>$user</em> and this is how you assigned a value to it.

```
$user = Get-AdUser ThmsRynr\n```

Using the Active Directory module, you got a specific user. Now, you want to report two properties back to the end user: SamAccountName and Enabled. The desired output looks like this:

```
The account ThmsRynr has enabled status of True.\n```

<!--more-->

So, you try something like this.

```
Write-Output "The account $user.SamAccountName has the enabled status of $user.Enabled"\n```

And you'll get something totally unexpected!

```
The account CN=ThmsRynr,OU=Users,DC=domain,DC=tld.SamAccountName has the enabled status of CN=ThmsRynr,OU=Users,DC=domain,DC=tld.Enabled\n```

Whaaaat? That's not what we want. What happened? It looks like I got the distinguished name of the user and then literally ".SamAccountName" and ".Enabled". Doesn't PowerShell know that I actually want the SamAccountName and Enabled properties?

Well, the short answer is no, PowerShell doesn't know that. What if you had a variable <em>$domain</em> set to "workingsysadmin" and wanted to do <strong>Write-Output "$domain.com"</strong> to get "workingsysadmin.com" written out? PowerShell doesn't know if you're trying to access a property on the variable, or work with .com (or .SamAccountName or .Enabled) as a literal string.

So what do we do? We'll use some brackets.

```
Write-Output "The account $($user.SamAccountName) has the enabled status of $($user.Enabled)"\n```

This will give the desired output. What we've done is use <strong>$( )</strong> to tell PowerShell that we want to evaluate the entire expression wrapped in those brackets, and use that in our string.
