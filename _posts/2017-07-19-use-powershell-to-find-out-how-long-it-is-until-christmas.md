---
layout: post
title: Use PowerShell To Find Out How Long It Is Until Christmas
date: 2017-07-19 07:00
author: thmsrynr@outlook.com
comments: true
categories: [beginner series, beginner series, christmas, datetime, datetime, get-date, PowerShell, powershell]
---
It's July at the time of this post, which means Christmas is right around the corner! Maybe not. How long is it until Christmas, anyway? Well, PowerShell can tell us if we get the date of Christmas and subtract today's date from it.

<!--more-->

```
PS&gt; (Get-Date 'December 25') - (Get-Date)


Days              : 202
Hours             : 15
Minutes           : 5
Seconds           : 13
Milliseconds      : 808
Ticks             : 175071138085639
TotalDays         : 202.628632043564
TotalHours        : 4863.08716904553
TotalMinutes      : 291785.230142732
TotalSeconds      : 17507113.8085639
TotalMilliseconds : 17507113808.5639
```

Only 17507113808.5639 more milliseconds until Christmas!
