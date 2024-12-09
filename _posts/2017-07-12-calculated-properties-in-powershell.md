---
layout: post
title: Calculated Properties in PowerShell
date: 2017-07-12 07:00
author: thmsrynr@outlook.com
comments: true
categories: [beginner series, beginner series, calculated properties, PowerShell, poweshell, select-object]
---
Most of the time, a PowerShell cmdlet will return all the information you need to work with it later in the pipeline. Sometimes, though, there's some assembly required. What I mean, is maybe the cmdlet returned the information you need, but not in the format you want, or you wish you had some property multiplied by some other property. Let's explore.

<!--more-->

Say you ran <strong>Get-ChildItem</strong> to get some items in a directory, and you get something like the following.

```
PS&gt; Get-ChildItem c:\temp\demo


    Directory: C:\temp\demo


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----         6/5/2017   8:40 AM        1519200 thing.txt
```

One of the items is Length, which tells you the size of the file in bytes. What if I wanted that in kilobytes, though? Well, it's not too hard. We're going to use a calculated property, using <strong>Select-Object</strong>.

```
PS&gt; Get-ChildItem c:\temp\demo | Select-Object -Property Name, @{label = 'FileSize'; expression = { $_.Length/1KB }}

Name        FileSize
----        --------
thing.txt 1483.59375
```

So I'm selecting two properties. One is Name, and the other is a calculated property. A calculated property is basically a hashtable with two items in it: a label, which is the name of our calculated property, and expression, which is the scriptblock that defines our calculation.

In this case, the name of my calculated property is FileSize, and the calculation is "the length of the item, divided by 1KB". In these calculations, <em>$_</em> basically refers to "the item we're looking at".
