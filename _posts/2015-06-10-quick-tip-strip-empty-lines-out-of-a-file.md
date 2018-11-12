---
layout: post
title: Quick Tip - Strip Empty Lines Out Of A File
date: 2015-06-10 08:30
author: thmsrynr@outlook.com
comments: true
categories: [PowerShell, powershell, PowerShell ISE, powershell ise, quick tip, string manipulation]
---
Here's a quick one-liner that will remove all of the blank lines from a file.

```
get-content $PathToInput | % { if (-not [string]::IsNullOrWhiteSpace($_)) { $_ | out-file -append $PathToOutput } }
```

The first thing I do is get the content of the input file. This returns an array of each line in the file which I pipe into a foreach-object loop (alias %). In the if block, I'm detecting if the currently evaluated item is null or just white space. If it isn't, I append it to the output file.
