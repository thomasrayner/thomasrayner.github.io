---
layout: post
title: PowerShell Regex Example: Incrementing Matches
date: 2018-01-10 07:30
author: thmsrynr
comments: true
categories: [PowerShell, powershell, regex, regex, string manipulation, string manipulation]
---
In the PowerShell Slack, I recently answered a question along these lines. Say you have a string that reads "first thing {} second thing {}" and you want to get to "first thing {0} second thing {1}" so that you can use the <em>-f</em>  operator to insert values into those spots. For instance...
<pre class="lang:default decode:true ">"first thing {0} second thing {1}" -f $(get-date -format yyyy-MM-dd), $(get-random)
# Will return "first thing 2018-01-10 second thing &lt;a random number&gt;"</pre>
The question is: how can you replace the {}'s in the string to {&lt;current number&gt;}?

<!--more-->

You might think you could do something like this.
<pre class="lang:default decode:true">$string = 'first thing {} second thing {}'
$i = 0
[regex]::replace($string, "\{\}", {"{$($i)}"; $i++})</pre>
But you'd be disappointed.

If you're not sure what's going on, the <em>[regex]</em> accelerator has a <em>replace</em>  method that works like <em>-replace</em>  does. It takes three arguments: the string that is being worked on, the pattern being detected, and what to replace the pattern with. In this case, I gave it a scriptblock to replace it with the value of <em>$i</em>  and then increment the value of the variable by one. Unfortunately, it doesn't look like <em>$i</em>  gets incremented. Everything gets replaced with a <em>{0}</em>  instead of an incremented number.

Long story short, this is a <a href="https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_scopes?view=powershell-5.1" target="_blank" rel="noopener">PowerShell scoping</a> issue. If you make <em>$i</em>  a part of a bigger scope like global, script, or something that makes sense for your situation, you'll get the results you desire (global is probably not the best choice).
<pre class="lang:default decode:true ">$string = 'first thing {} second thing {}'
$global:i = 0
[regex]::replace($string, "\{\}", {"{$($global:i)}"; $global:i++})

#returns first thing {0} second thing {1}</pre>
And this will work just fine in your <em>-f</em>  replacement operations!
