---
layout: post
title: Regex Example - Strip Out HTML Tags
date: 2018-02-21 07:30
author: thmsrynr
comments: true
categories: [html, PowerShell, powershell, regex, regex, regular expressions, string manipulation, string manipulation]
---
First and foremost, HTML is <strong>not</strong> regex friendly. You should not try to parse HTML in PowerShell, or using regular expressions unless you've lost some kind of bet or want to punish yourself for something. PowerShell has things like <strong>ConvertTo-HTML</strong> that will make that kind of thing way less migraine inducing.

That said, I recently had a situation where I just wanted to strip all the HTML tags out of a string. My input looked something like this (assigned to a variable <em>$html</em>).
```
&lt;html&gt;
&lt;body&gt;
&lt;p&gt;This is an important value&lt;/p&gt;
&lt;/body&gt;
&lt;/html&gt;\n```
<!--more-->

All I want is the "This is an important value" part, so this seemed like a place where the "don't use regex on HTML" rule could be broken. It's even a pretty simple regex.
```
$html -replace '(&lt;\/*\w+?&gt;){1,}'\n```
You'll have to wrap it in round brackets and use a <strong>.trim()</strong> to clean up white space, but this will work for the "get rid of the HTML" goal. Let's break down this regular expression to see what it's doing.

Starting on the far right side, the <strong>{1,}</strong> is specifying "one or more" or the pattern that precedes it, in this case, the rest of the expression wrapped in round brackets. Inside those round brackets is a patter which states "an angle bracket (<strong>&lt;</strong>), zero or more forward slashes escaped by a back slash (<strong>\/*</strong>), as many alphanumeric characters as it takes (<strong>\w+?</strong>) to get to a closing angle bracket (<strong>&gt;</strong>)". It just rolls off the tongue, right?

Basically we're looking for any opening or closing HTML tag. We're not capturing some HTML, though like <strong>img</strong> or <strong>a </strong>tags that can have other values inside them (like <strong>&lt;img src="pic.png" /&gt;</strong>) but the regex in this example can easily be built upon to include examples like that, now that you've got this far. You could even just replace the <strong>\w</strong> with <strong>[^&gt;]</strong> which means "any character except a closing angel bracket".

Happy regexing!
