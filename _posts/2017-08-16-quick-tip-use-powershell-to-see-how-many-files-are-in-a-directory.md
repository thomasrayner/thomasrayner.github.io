---
layout: post
title: Quick Tip - Use PowerShell To See How Many Files Are In A Directory
date: 2017-08-16 07:00
author: thmsrynr@outlook.com
comments: true
categories: [active directory, active directory, activedirectory, beginner series, beginner series, count, get-childitem, PowerShell, powershell, quick tip, working with objects]
---
Here's a way to see how many files are in a directory, using PowerShell.

<!--more-->

As you likely know, you can use <strong>Get-ChildItem</strong> to get all the items in a directory. Did you know, however, that you can have PowerShell quickly count how many files there are?

<pre class="lang:ps decode:true">PS&gt; (Get-ChildItem -Path c:\temp\demo).count
3</pre>

I probably could have counted the files in this specific directory pretty easily myself, since there's only 3 of them. If you want to see how many files are in an entire folder structure, use the <em>-Recurse</em> flag to go deeper.

You can do this with any output from a cmdlet when it's returned in an array of objects. Check this out.

<pre class="lang:ps decode:true">PS&gt; (Get-AdUser -filter "Name -like 'Thomas *'").count
7</pre>

In my test Active Directory, there are 7 AD users with a name that matches the pattern "Thomas *".
