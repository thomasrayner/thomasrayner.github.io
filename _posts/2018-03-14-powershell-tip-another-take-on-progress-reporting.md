---
layout: post
title: PowerShell Tip - Another Take On Progress Reporting
date: 2018-03-14 07:30
author: thmsrynr
comments: true
categories: [ansi, ansi, PowerShell, powershell, string manipulation, string manipulation]
---
Normally in PowerShell if you want to report progress on a long running task, you'd use a progress bar using the <strong>Write-Progress</strong> cmdlet. That's definitely the right way to do this, but what if you wanted a different way... for some reason? In the PowerShell Slack (invite yourself: <a href="http://slack.poshcode.org" target="_blank" rel="noopener">slack.poshcode.org</a>), I recently answered this question: "I want to write out 'There are 3 seconds remaining. There are 2 seconds remaining.' etc. until there are no seconds remaining and then keep going, but I don't want them all to appear on the different lines. I basically just want the number to update."

This gif shows what the question asker was after (except instead of counting up, they wanted a countdown).

<!--more-->

<img class="alignnone size-full wp-image-709" src="/wp-content/uploads/2018/03/countdown.gif" alt="" width="296" height="116" />

So, then, how do we get that? Well, the answer is <a href="https://en.wikipedia.org/wiki/ANSI_escape_code" target="_blank" rel="noopener">ANSI Escape Sequences</a>! These are encoded instructions included in a string to direct the console about how to change or manipulate the output. I use them in my prompt.

First, let's just get our countdown - er, I mean count<em>up</em>... working. This is pretty straight forward.
```
1..10 | % { "There are $_ s remaining"; start-sleep -seconds 1 }\n```
This will write everything on its own line, like this.
```
There are 1 s remaining
There are 2 s remaining
There are 3 s remaining
There are 4 s remaining
There are 5 s remaining
There are 6 s remaining
There are 7 s remaining
There are 8 s remaining
There are 9 s remaining
There are 10 s remaining\n```
Now, for the fanciness, what we really want is for the same line to get overwritten.

You can write an ESC inside of a string just like you would any other character. It's represented by char 27. So we'll set that equal to a variable <strong>$E.</strong>
```
$E = [char]27\n```
Now we can embed it in strings, and we just need the rest of the sequence. If you scroll enough on that Wikipedia page linked above, you'll get to the CSI sequences section, which basically all start with the escape character and then an open square bracket (this character: <strong>[</strong>). At the bottom of the table, you'll notice <strong>s</strong> and <strong>u</strong> sequences for saving and restoring the cursor position.

So all we need to do is save the cursor position when we start, and then restore it each time we want to overwrite the line.
```
"${E}[s"
1..10 | % { "${E}[uThere are $_ s remaining"; Start-Sleep -Seconds 1 }\n```
On the first line, all I'm doing is saving the cursor position. I wrap the E in $E in curly braces so it doesn't think the square brace or the s is part of the name of the variable. You don't <em>have</em> to do this for this escape sequence since the square brace isn't a valid character in a variable name, but for some other ANSI stuff, you might want to get into this habit.

Then on the next line, I've just got a foreach-object loop (alias is %) that writes the same line over and over and sleeps for one second. The line it writes restores the cursor position to the one that was saved on the line above and then just writes "There are x s remaining". We're overwriting the same line over and over.

This works in our scenario because the line we're writing text of the same length or longer. If you want to see this activity look a little odd, you can try something like this.
```
"${E}[sHello"
start-sleep -seconds 1
"${E}[uHi"\n```
We're saving the cursor position, writing "Hello", waiting a second, then restoring the cursor position and writing "Hi". We'll see "Hello" for a second then the resulting line that comes afterwards looks like this.
```
Hillo\n```
This happens because we restored the cursor position and just started writing more characters. So, be careful of this if you're using this trick in your own scripts. You can use the .PadRight() and .PadLeft() methods that are built into strings to try to fix this, or something more dynamic like detect the length of the strings you're writing.
```
"${E}[sHello"
start-sleep -seconds 1
"${E}[uHi".PadRight(20)\n```
Notice on the last line, I'm using the .PadRight() method to add 20 characters of whitespace which will overwrite all of the rest of the text that wasn't being overwritten before.
