---
layout: post
title: Quick Tip - Validate The Length Of An Integer
date: 2016-12-07 08:30
author: thmsrynr@outlook.com
comments: true
categories: [int, PowerShell, powershell, quick tip, quicktip, regex, regex]
---
A little while ago, I fielded a question in the <a href="http://powershell.slack.com/" target="_blank">PowerShell Slack channel</a> which was “How do I make sure a variable, which is an int, is of a certain length?”

Turns out it’s not too hard. You just need to use a little regex. Consider the following example.

```
[int]$v6 = 849032
[int]$v2 = 23
$v6 -match '^\d{6}$'
$v2 -match '^\d{6}$'\n```

<strong>$v6</strong> is an int that is six digits long. <strong>$v2</strong> is an int that is only two inches long. On lines three and four, we're testing to see if each variables match the pattern <em>'^\d{6}$'</em> which is regex speak for "start of the line, any digit, and six of them, end of the line". The first one will be true, because it's six digits, and the second one will be false. You could also use something like <em>'^\d{4,6}$'</em> to validate that the int is between four and six digits long.
