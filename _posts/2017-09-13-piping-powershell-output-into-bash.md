---
layout: post
title: Piping PowerShell Output Into Bash
date: 2017-09-13 07:00
author: thmsrynr@outlook.com
comments: true
categories: [bash, bash, beginner series, filesystem, PowerShell, powershell, quick tips, string manipulation]
---
With Windows 10, you can<a href="https://msdn.microsoft.com/en-us/commandline/wsl/install_guide" target="_blank" rel="noopener noreferrer"> install Bash on Windows</a>. Cool, right? Having Bash on Windows goes a long way towards making Windows a more developer-friendly environment and opens a ton of doors. The one I'm going to show you today is more of a novelty than anything else, but maybe you'll find something neat to do with it.

<!--more-->

If you've been around PowerShell, you're used to seeing the pipe character ( | ) used to pass the output from one command into the input of another. What you can do now, kind of, is pass the output of a PowerShell command into the input of a Bash command. Here's an example. Get ready for this biz.

```
Get-ChildItem c:\temp\demo | foreach-object { bash -c "echo $($_.Name) | awk /\.csv/" }
```

In my c:\temp\demo folder, I have three files, two of which are CSVs. In an attempt to be super inefficient, I am piping the files in that directory into a <strong>foreach-object</strong> loop and using Bash to tell me which ones end in .csv, using <strong>awk</strong>. This is hardly the best way to do this, but it gives you an idea of how you can start to intermingle these two shells.
