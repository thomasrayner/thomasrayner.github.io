---
layout: post
title: Beginner PowerShell Tip - Using Variable Properties In Strings
date: 2017-11-29 07:00
author: thmsrynr@outlook.com
comments: true
categories: [active directory, beginner series, beginner series, PowerShell, powershell, string manipulation, string manipulation, strings]
---
If you're just getting started in PowerShell, it's possible that you haven't bumped into this specific issue yet. Say you've got a variable named <em>$user</em> and this is how you assigned a value to it.

<pre class="lang:ps decode:true ">$user = Get-AdUser ThmsRynr</pre>

Using the Active Directory module, you got a specific user. Now, you want to report two properties back to the end user: SamAccountName and Enabled. The desired output looks like this:

<pre class="lang:ps decode:true ">The account ThmsRynr has enabled status of True.</pre>

<!--more-->

So, you try something like this.

<pre class="lang:ps decode:true ">Write-Output "The account $user.SamAccountName has the enabled status of $user.Enabled"</pre>

And you'll get something totally unexpected!

<pre class="lang:ps decode:true ">The account CN=ThmsRynr,OU=Users,DC=domain,DC=tld.SamAccountName has the enabled status of CN=ThmsRynr,OU=Users,DC=domain,DC=tld.Enabled</pre>

Whaaaat? That's not what we want. What happened? It looks like I got the distinguished name of the user and then literally ".SamAccountName" and ".Enabled". Doesn't PowerShell know that I actually want the SamAccountName and Enabled properties?

Well, the short answer is no, PowerShell doesn't know that. What if you had a variable <em>$domain</em> set to "workingsysadmin" and wanted to do <strong>Write-Output "$domain.com"</strong> to get "workingsysadmin.com" written out? PowerShell doesn't know if you're trying to access a property on the variable, or work with .com (or .SamAccountName or .Enabled) as a literal string.

So what do we do? We'll use some brackets.

<pre class="lang:ps decode:true ">Write-Output "The account $($user.SamAccountName) has the enabled status of $($user.Enabled)"</pre>

This will give the desired output. What we've done is use <strong>$( )</strong> to tell PowerShell that we want to evaluate the entire expression wrapped in those brackets, and use that in our string.
