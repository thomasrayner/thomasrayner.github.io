---
layout: post
title: Use PowerShell to Figure Out "What day of the week is it 39 (or some other number) days from now?"
date: 2017-07-05 07:00
author: thmsrynr@outlook.com
comments: true
categories: [beginner series, beginner series, datetime objects, PowerShell, powershell, Uncategorized]
---
There's lots of fun things you can do with datetime objects in PowerShell, and using the <strong>Get-Date</strong> cmdlet. Here's one of them.

<!--more-->

Say you want to know what day of the week it will be some arbitrary number of days from now. It's pretty easy.

<pre class="lang:ps decode:true ">PS&gt; (Get-Date).AddDays(39).DayOfWeek
Friday</pre>

At the time I write this, it looks like in 39 days, it'll be Friday.
