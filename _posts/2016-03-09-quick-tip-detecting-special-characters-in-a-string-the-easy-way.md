---
layout: post
title: Quick Tip - Detecting Special Characters In A String The Easy Way
date: 2016-03-09 08:30
author: thmsrynr@outlook.com
comments: true
categories: [detect special char, PowerShell, powershell, quick tip]
---
Here's a super easy way to detect special characters in a string. Consider the following.

```
$string1 = 'something'
$string2 = 'some@thing'

$string1 -eq $($string1 -replace '[^a-zA-Z]','')
$string2 -eq $($string2 -replace '[^a-zA-Z]','')\n```

String1 has no special characters, String2 does. All I'm doing is comparing the string to "the string if we replace everything that isn't a regular letter" using the -replace operator.

It's just that easy.

You could do the same thing with the -match operator, too. The point here is looking at the regex.

```
$string -match '[^a-zA-Z]'\n```
