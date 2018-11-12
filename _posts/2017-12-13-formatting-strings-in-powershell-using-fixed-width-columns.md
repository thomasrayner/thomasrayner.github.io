---
layout: post
title: Formatting Strings In PowerShell Using Fixed Width Columns
date: 2017-12-13 07:00
author: thmsrynr@outlook.com
comments: true
categories: [PowerShell, powershell, string manipulation, string manipulation]
---
Working with strings in PowerShell is fun, I don't care what you say. In this post, I'm going to show you how to clean up the strings your code outputs, at least in some situations.

Say you have a variable <em>$fileExtensions</em> which you populated with this command.
<pre class="lang:ps decode:true">PS&gt; $fileExtensions = Get-ChildItem | Group-Object -Property Extension</pre>
And, for some reason, instead of the default output which is formatted like a table, I want output presented like this.

<!--more-->
<pre class="lang:ps decode:true ">.ps1     file extension: 11
.xlsx    file extension: 3
.dll     file extension: 1</pre>
This is a silly example, but notice that even though there are extensions of varying length (.ps1 and .dll are four characters including the dot, and .xlsx is five), all of the "file extension: &lt;number&gt;" is aligned.

How'd I do that? Let's start with some code that <em>doesn't</em> work.
<pre class="lang:ps decode:true ">PS&gt; $fileExtensions | foreach-object { "$($_.Name) file extension: $($_.Count)" }

.ps1 file extension: 11
.xlsx file extension: 3
.dll file extension: 3</pre>
How incredibly unfortunately unattractive! Luckily, it's not too hard to fix. Check out this code.
<pre class="lang:ps decode:true">PS&gt; $fileExtensions | foreach-object { "{0,-8} file extension: {1}" -f $_.Name, $_.Count }


.ps1     file extension: 11
.xlsx    file extension: 3
.dll     file extension: 3</pre>
Oh yes look at that goodness. In this example I'm using the <em>-f </em> operator to insert the variables into the string. Let's break down the new string I'm creating.

<em>{0}</em> and <em>{1]</em> are basically placeholders. The <em>-f</em> operator is going to insert the variables that come after it (<em>$_.Name</em> and <em>$_.Count</em>) into the 0 and 1 spots.

The <em>,-8</em> is a formatting instruction. The 8 means that this part of the string is going to be a column that takes up 8 characters worth of space. The negative sign means that the data inserted is left aligned. If I had used "positive eight" it would have been right aligned.

Now you can take this and run, to do fun things like this.
<pre class="lang:ps decode:true "># Input
$header = "[$(Get-Date -format G)]"
Write-Output "$header First line"
Write-Output $("{0,$($header.Length)} Second line" -f " ")
Write-Output $("{0,$($header.Length)} Third line" -f " ")

# Output

[11/2/2017 12:47:58 PM] First line
                        Second line
                        Third line</pre>
