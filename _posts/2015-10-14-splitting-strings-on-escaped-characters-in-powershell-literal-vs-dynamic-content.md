---
layout: post
title: Splitting Strings On Escaped Characters In PowerShell - Literal vs. Dynamic Content
date: 2015-10-14 08:30
author: thmsrynr@outlook.com
comments: true
categories: [escape characters, PowerShell, powershell, PowerShell ISE, powershell ise, splitting strings, string manipulation]
---
Before we get into this post, here's a little required reading: <a href="http://blogs.technet.com/b/heyscriptingguy/archive/2015/06/20/weekend-scripter-understanding-quotation-marks-in-powershell.aspx" target="_blank">http://blogs.technet.com/b/heyscriptingguy/archive/2015/06/20/weekend-scripter-understanding-quotation-marks-in-powershell.aspx</a>

This is a "Hey, Scripting Guy!" post by Don Walker about using single vs. double quotes to wrap strings and other items ( ' vs. " ). The bottom line is that single quotes should be your default go-to and denote a literal string. Double quotes are only to be used when dynamic content is involved. It's all explained quite clearly in the post linked above.

Awesome information, but, it doesn't talk about escape characters. In PowerShell the backtick character ( ` ) - the one you hit along with shift to get the tilde character ( ~ ) on most keyboards - is what's known as an escape character. Here's some <a href="https://technet.microsoft.com/en-us/library/hh847755.aspx?f=255&amp;MSPPError=-2147217396" target="_blank">more reading on escape characters</a> if you're unfamiliar.

Now, what if I have something like this?

<pre class="lang:ps decode:true ">$Body = 'Thank you for stopping by to see us.

It was nice to see you.

Stop by again soon.

Thanks!'</pre>

It's just a multi-line string with blank lines in between each of the lines with content. Now, what if I wanted to keep each of the content lines on it's own line while removing all the lines that are blank? Well, since $Body is one big multi-line string, I can split it on "new line". Using escape characters in PowerShell, to denote a new line we just type:

<pre class="">`r`n</pre>

So can I do this?

<pre class="lang:ps decode:true">Write-Host 'Using single quotes' -ForegroundColor Green
$Body.split('`r`n') | % { if (-not [string]::IsNullOrWhiteSpace($_)) { $_ } }</pre>

I'm splitting $Body on each new line, and for each line, if it is not null or white space (<a href="http://www.workingsysadmin.com/quick-tip-strip-empty-lines-out-of-a-file/" target="_blank">using some of the information from this post</a>), I write it. I'm using single quotes to wrap the new line marker to split up $Body. Well, unfortunately, the output looks like this.

<a href="http://www.workingsysadmin.com/wp-content/uploads/2015/06/6-30-2015-8-37-49-AM.png"><img class="alignnone size-full wp-image-268" src="http://www.workingsysadmin.com/wp-content/uploads/2015/06/6-30-2015-8-37-49-AM.png" alt="Splitting Strings 1" width="175" height="274" /></a>

Well, that's not exactly what I was hoping for. Instead of splitting $Body on a new line, it looks like it's split it on the letters n and r. It turns out that the escape character, like variables and the output from commands, is dynamic content. To do what I'm trying to do, the command needs to look like this.

<pre class="lang:ps decode:true ">Write-Host 'Using double quotes' -ForegroundColor Green
$Body.split("`r`n") | % { if (-not [string]::IsNullOrWhiteSpace($_)) { $_ } }</pre>

The only difference is the value in the split command. Instead of single quotes I've got double quotes wrapping the new line marker. Now the output looks like this.

<a href="http://www.workingsysadmin.com/wp-content/uploads/2015/06/6-30-2015-8-41-42-AM.png"><img class="alignnone size-full wp-image-269" src="http://www.workingsysadmin.com/wp-content/uploads/2015/06/6-30-2015-8-41-42-AM.png" alt="Splitting Strings 2" width="297" height="99" /></a>

Perfect! So remember, escape characters are dynamic content. They are not considered part of a literal string.
