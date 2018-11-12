---
layout: post
title: Quick Tip - PowerShell Supports Partial Parameter Names
date: 2018-03-21 07:30
author: thmsrynr
comments: true
categories: [beginner series, beginner series, PowerShell, powershell, quick tip, quick tips]
---
Did you know that PowerShell supports the usage of partial parameter names? This isn't such a big deal since tab completion is a thing... and if you're writing code, you want to use the full parameter name to provide clarity and readability... but sometimes this is handy. Whether it's for code golf, or just noodling around in the console, you don't have to specify the full name of a parameter, just enough for it to be unique.

Here are some examples.

<!--more-->
```
Get-ChildItem -Pa c:\temp
# Pa is matching the Path parameter
# Note if you just do P, you'll be told that the parameter can't be processed and a list of possible matches\n```
```
Get-CimInstance -Clas win32_operatingsystem
# Clas is part of the ClassName parameter\n```
Obviously this isn't something that you should be running wild with and using in all your production code, but maybe it'll explain how some random code you found on the internet works.
