---
layout: post
title: Quick Tip - When was an Exchange Online Protection Transport Rule Changed?
date: 2015-02-04 02:00
author: thmsrynr@outlook.com
comments: true
categories: [eop, Exchange, exchange, Exchange Online Protection, exchange online protection, PowerShell, powershell, PowerShell ISE, powershell ise]
---
What if you have an Exchange Online Protection (EOP) transport rule that isn't behaving the way you thought it should? I've been the victim of some strange inconsistencies with EOP since they tried to migrate us from Forefront Online Protection for Exchange (FOPE) in March (actually summer) of last year.

So did a transport rule get changed administratively by some cowboy admin colleague? Or is EOP conspiring against you? In EOP's GUI, you can't tell when a transport rule was changed last but you can if you <a title="Quick Tip: Opening An Exchange Online Protection Shell" href="http://www.workingsysadmin.com/quick-tip-opening-an-exchange-online-protection-shell/" target="_blank">make a remote connection to EOP using PowerShell</a>.

You just need to know the name which you can find by running a <strong>Get-TransportRule</strong> command and looking for the one that you're interested in. Then run this...

```
(Get-TransportRule | ? { $_.Name -eq 'The Name Of Your Rule' }).WhenChanged
```

... which will give you the date and time that the rule was last changed.
