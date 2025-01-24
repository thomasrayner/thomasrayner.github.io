---
layout: post
title: Imported PowerShell Sessions ErrorActionPreference Gotcha
date: 2015-03-25 08:30
author: thmsrynr@outlook.com
comments: true
categories: [Exchange, exchange, gotcha, PowerShell, powershell, PowerShell ISE, powershell ise, quick tip]
---
I just bumped into something silly that I know I'll forget about in the future. Using the <a title="Opening A Remote Exchange Management Shell" href="http://www.workingsysadmin.com/opening-a-remote-exchange-management-shell/" target="_blank">function in my PowerShell profile to open an Exchange Management shell</a>, I ran the following command as part of a script.

```
try { Get-Recipient doesntexist } catch [Exception]{ write-line "No such mailbox" }
```

It's a pretty self-explanatory command. I was trying to detect if a mailbox, in this case "doesntexist", existed or not. Typically if the mailbox doesn't exist, the <strong>Get-Recipient</strong> cmdlet will throw an error. My goal was to catch the error and do something productive with it but the above command doesn't trigger the Catch block.

No problem, I thought to myself. My ErrorActionPreference is set to Continue by default so I'll tweak it for this command.

```
try { Get-Recipient doesntexist -erroraction stop } catch [Exception]{ write-line "No such mailbox" }
```

The <strong>-ErrorAction Stop</strong> part should make the script stop executing on an error and hop into the Catch block. Wrong! The above command throws an error without triggering the Catch block, too.

It turns out I had to edit my <strong>$ErrorActionPreference</strong> variable to be <strong>Stop</strong>. Just using the flag in the command doesn't work. I've run into this in other scripts where I import a PSSession, too. Now my command looks something like this.

```
Try { $OldErrorActionPref = $ErrorActionPreference; $ErrorActionPreference = "Stop"; Get-Recipient doesntexist } catch [Exception]{ write-host "No such mailbox" } $ErrorActionPreference = $OldErrorActionPref

```

First, I'm getting the current value of <b>$ErrorActionPreference</b> and storing it. Then I set the ErrorActionPreference to <strong>Stop</strong>. I run my <strong>Get-Recipient</strong> command which fails and <em>now</em> instead of getting an error, my Catch block is triggered. Afterwards, I set <strong>$ErrorActionPreference</strong> back to it's previous value.

Now, because I've written a blog post about this, I'll never forget again.
