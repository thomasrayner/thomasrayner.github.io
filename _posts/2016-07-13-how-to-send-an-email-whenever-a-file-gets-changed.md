---
layout: post
title: How To Send An Email Whenever A File Gets Changed
date: 2016-07-13 08:30
author: thmsrynr@outlook.com
comments: true
categories: [Automation, filesystem, filesystem, PowerShell, powershell, slack]
---
A little while ago, I fielded a question in the <a href="http://powershell.slack.com" target="_blank">PowerShell Slack channel</a> which was "How do I send an email automatically whenever a change is made to a specific file?"

Turns out it's not too hard. You just need to set up a file watcher.

```
$watcher = New-Object System.IO.FileSystemWatcher
$watcher.Path = 'C:\temp\'
$watcher.Filter = 'test1.txt'
$watcher.EnableRaisingEvents = $true

$changed = Register-ObjectEvent $watcher 'Changed' -Action {
   write-output "Changed: $($eventArgs.FullPath)"
}
```

First, we create the watcher, which is just a FileSystemWatcher object. Technically the watcher watches the whole directory for changes (the path), which is why we add a filter.

Then we register an ObjectEvent, so that whenever the watcher sees a change event, it performs an action. In this case, I just have it writing output but it could easily be sending an email or performing some other task.

To get rid of the ObjectEvent, just run the following.

```
Unregister-Event $changed.Id
```

It's just that easy!
