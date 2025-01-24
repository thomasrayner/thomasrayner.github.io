---
layout: post
title: Quick Script Share - Prompt To Copy File If It Already Exists
date: 2016-11-16 08:30
author: thmsrynr@outlook.com
comments: true
categories: [copy-item, filesystem, PowerShell, powershell]
---
By default, <strong>Copy-Item</strong> will overwrite a file if it exists, unless that file is marked Read Only (in which case you can use the <em>-Force</em> switch to overwrite the file). What if you want to only copy the file if it doesn't exist, though? What then?

Well, then do this:

<script src="https://gist.github.com/ThmsRynr/1c671eb31a95878cc7bcf32608c90a80.js"></script>
