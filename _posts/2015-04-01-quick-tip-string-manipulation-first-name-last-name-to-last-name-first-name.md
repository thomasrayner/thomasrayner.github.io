---
layout: post
title: Quick Tip - String Manipulation - First Name Last Name to Last Name, First Name
date: 2015-04-01 08:30
author: thmsrynr@outlook.com
comments: true
categories: [PowerShell, powershell, PowerShell ISE, powershell ise, string manipulation]
---
I've got kind of a silly post this week. I often get a list of names in the format...

<blockquote>
<p style="padding-left: 30px;">John Doe</p>
<p style="padding-left: 30px;">Jane Doe</p>
<p style="padding-left: 30px;">Mike Smith</p>
<p style="padding-left: 30px;">Mary Smith</p>
</blockquote>

... that I actually need to be in the format...

<blockquote>
<p style="padding-left: 30px;">Doe, John; Doe, Jane; Smith, Mike; Smith, Mary</p>
</blockquote>

... and sometimes, especially with long lists of names, it's a pain to do the manipulation in Notepad or Word. So what do you think I did? That's right, I wrote a PowerShell script to handle it for me. I just throw the list of people into a text file and call up this script.

<pre class="lang:ps decode:true ">$rawnames = get-content C:\path\to\names.txt
$csnames = ""
$rawnames | % { $csnames += "$($_.tostring().split(' ')[1]), $($_.tostring().split(' ')[0]); "}
$csnames | clip.exe</pre>

This isn't the tidiest script but I break it up into a couple extra parts so it's easier to edit on the fly. I might comment out the " | clip.exe " part of the last line if I don't want the output on my clipboard.

The first line just gets the content of the text file and the second line initializes the variable <strong>$csnames</strong> (which stands for [semi]colon separated names). On the third line, I go through every value in the text file and put the part after the first space (the last name), a comma and space, and then the part before the first space (the first name) into the <strong>$csnames</strong> string. I throw a semicolon on and move to the next one.

This won't do well with names like "John van Doe" that have multiple spaces. It just happens to suit my needs and might serve as a super simple example to some of you who are trying to wrap your heads around manipulating strings in PowerShell.
