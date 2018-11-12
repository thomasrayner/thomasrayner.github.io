---
layout: post
title: New in PowerShell 6 - Positive And Negative Parameter Validation
date: 2018-05-30 07:30
author: thmsrynr
comments: true
categories: [parameter validation, PowerShell, powershell, powershell 6, powershell 6]
---
If you've written at least a couple of advanced PowerShell functions, you're probably no stranger to parameter validation. These are the attributes you attach to parameters to make sure that they match a certain regular expression using [ValidatePattern()], or that when they are plugged into a certain script, that it evaluates to true using [ValidateScript({})]. You've probably also used [ValidateRange()] to make sure a number falls between a min and a max value that you specified.

In PowerShell 6, though, there's something new and cool you can do with ValidateRange. You can specify in a convenient new syntax that the value must be positive or negative.

<!--more-->

To do this, you start with a normal ValidateRange attribute, and instead of providing a range of numbers, you just use the word "Positive" or "Negative", like this.
```
[ValidateRange('Positive')]$int = 10
[ValidateRange('Negative')]$int = -10\n```
These will both work correctly because we're assigning a value that works with the validation we've specified. Here's two that will throw errors.
```
[ValidateRange('Positive')]$int = -10
[ValidateRange('Negative')]$int = 10\n```
Here's what it looks like in the console.

<img class="alignnone size-full wp-image-762" src="/wp-content/uploads/2018/05/2018-05-15-09_32_19-PowerShell-6.0.0.png" alt="" width="835" height="356" />

Neat, right?
