---
layout: post
title: Finding Out When A PowerShell Cmdlet Was Introduced
date: 2018-07-18 07:30
author: thmsrynr
comments: true
categories: [docs, github, open source, PowerShell, powershell]
---
In the PowerShell Slack (<a href="https://bit.ly/psslack" target="_blank" rel="noopener">invite yourself at bit.ly/psslack</a>), there was a very brief debate over when the <strong>Expand-Archive</strong> cmdlet was introduced to PowerShell. This is absolutely information that can be found online, but there's a few different ways.

Some cmdlets have this information built into the help, some share this information in the online docs. Since the core cmdlets documentation are open sourced and on GitHub, however, you can go straight to the source and quickly answer this question for yourself.

<!--more-->

If you go to <a href="https://github.com/powershell/powershell-docs" target="_blank" rel="noopener">https://github.com/powershell/powershell-docs</a>, you'll find all the documentation for the core PowerShell cmdlets. In the Reference folder, you'll see documentation for all the currently supported versions of PowerShell (back to 3.0). The docs for older cmdlets are in there too, but typically you're going to be looking for if a cmdlet was introduced in version 4 or 5, in my experience.

Click on the Find File button in GitHub, and you'll be presented with a search screen.

<img class="alignnone wp-image-792 size-full" src="/wp-content/uploads/2018/07/2018-07-16-08_55_35-PowerShell_PowerShell-Docs_-The-official-PowerShell-documentation-sources-e1531756898953.png" alt="" width="578" height="224" />

<img class="alignnone size-large wp-image-789" src="/wp-content/uploads/2018/07/2018-07-16-08_52_08-PowerShell-Docs_reference-at-staging-·-PowerShell_PowerShell-Docs-1024x353.png" alt="" width="604" height="208" />From there, type in the name of the cmdlet, and the search will start to populate. Let's see when the <strong>Expand-Archive</strong> cmdlet was introduced.

<img class="alignnone size-large wp-image-790" src="/wp-content/uploads/2018/07/2018-07-16-08_54_22-File-Finder-1024x381.png" alt="" width="604" height="225" />

You can see that this core cmdlet is in the docs for versions 5.0, 5.1 and 6. That means that we can assume this cmdlet was introduced in PowerShell version 5.
