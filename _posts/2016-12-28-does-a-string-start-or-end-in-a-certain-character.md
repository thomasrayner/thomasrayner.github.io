---
layout: post
title: Does A String Start Or End In A Certain Character?
date: 2016-12-28 08:30
author: thmsrynr@outlook.com
comments: true
categories: [filesystem, filesystem, PowerShell, powershell, regex, regex, string manipulation, string manipulation]
---
Can you tell in PowerShell if a string ends in a specific character, or if it starts in one? Of course you can. Regex to the rescue!

It's a pretty simple task, actually. Consider the following examples

```
'something\' -match '.+?\\$'
#returns true

'something' -match '.+?\\$'
#returns false

'\something' -match '^\\.+?'
#returns true

'something' -match '^\\.+?'
#returns false
```

In the first two examples, I'm checking to see if the string ends in a backslash. In the last two examples, I'm seeing if the string starts with one. The regex pattern being matched for the first two is <strong>.+?&#92;$ </strong>. What's that mean? Well, the first part <strong>.+?</strong> means "any character, and as many of them as it takes to get to the next part of the regex. The second part \<strong>&#92;</strong> means "a backslash" (because \ is the escape character, we're basically escaping the escape character. The last part <strong>$</strong> is the signal for the end of the line. Effectively what we have is "anything at all, where the last thing on the line is a backslash" which is exactly what we're looking for. In the second two examples, I've just moved the \<strong>&#92;</strong> to the start of the line and started with <strong>^</strong> instead of ending with <strong>$</strong> because <strong>^</strong> is the signal for the start of the line.

Now you can do things like this.

```
$dir = 'c:\temp'
if ($dir -notmatch '.+?\\$')
  {
    $dir += '\'
  }
$dir
#returns 'c:\temp\'
```

Here, I'm checking to see if the string 'bears' ends in a backslash, and if it doesn't, I'm appending one.

Cool, right?
