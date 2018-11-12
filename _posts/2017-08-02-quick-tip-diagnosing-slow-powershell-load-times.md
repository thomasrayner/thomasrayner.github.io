---
layout: post
title: Quick Tip - Diagnosing Slow PowerShell Load Times
date: 2017-08-02 07:00
author: thmsrynr@outlook.com
comments: true
categories: [beginner series, beginner series, PowerShell, powershell, quick tip, Uncategorized]
---
I could write an entire book on "why does my PowerShell console take so long to load?" but I don't want to write that book. Instead, here's a way to make sure the reason your console is loading slowly isn't because of something dumb.

<!--more-->

When you launch PowerShell, one of the things that happens is that your profile is loaded. Your profile is basically its own script that runs to setup and configure your environment before you start using it. I use mine to define some custom aliases, functions, import some modules, and set my prompt up. You can see what your profile is doing by running <strong>notepad $profile</strong>. This will open your profile in notepad (but you can use the ISE or Visual Studio Code or Notepad++ etc. if you prefer).

There is more than one profile used by PowerShell depending on how you're running PowerShell, and $profile will always refer to the one that's currently applied to you. If you run that command above and are told that there's no such file, it means don't have anything configured in your PowerShell profile.

Keep in mind, there could be a lot of other reasons that your console loads slowly. This is just a quick way to clear out any dumb code from your profile.
