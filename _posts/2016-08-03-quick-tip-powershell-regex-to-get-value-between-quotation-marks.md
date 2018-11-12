---
layout: post
title: Quick Tip - PowerShell Regex To Get Value Between Quotation Marks
date: 2016-08-03 08:30
author: thmsrynr@outlook.com
comments: true
categories: [PowerShell, powershell, regex, regex, string manipulation, string manipulation]
---
If you've got a value like the following...

```
$s = @"
Here is: "Some data"
Here's "some other data"
this is "important" data
"@\n```

... that maybe came from the body of a file, was returned by some other part of a script, etc., and you just want the portions that are actually between the quotes, the quickest and easiest way to get it is through a regular expression match.

That's right, forget splitting or trimming or doing other weird string manipulation stuff. Just use the <strong>[regex]::matches() </strong>feature of PowerShell to get your values.

```
[regex]::matches($s,'(?&lt;=\").+?(?=\")').value\n```

<strong>Matches</strong> takes two parameters. 1. The value to look for matches in, in this case the here-string in my $s variable, and 2. The regular expression to be used for matching. Since <strong>Matches</strong> returns a few items, we are making sure to just select the value for each match.

So what is that regex doing? Let's break it down into it's parts.

<ul>
    <li><strong>(?&lt;=\")</strong> this part is a look behind as specified by the<strong> ?&lt;=</strong> part. In this case, whatever we are matching will come right after a quote. Doing the look behind prevents the quotation mark itself from actually being part of the matched value. Notice I have to escape the quotation mark character.</li>
    <li><strong>.+?</strong> this part basically matches as many characters as it takes to get to whatever the next part of the regex is. Look into regex lazy mode vs greedy mode.</li>
    <li><strong>(?=\")</strong> this part is a look ahead as specified by the <strong>?=</strong> part. We're looking ahead for a quotation mark because whatever comes after our match is done will be a quotation mark.</li>
</ul>

So basically what we've got is "whatever comes after a quotation mark, and as much of that as you need until you get to another quotation mark". Easy, right? Don't you love regex?
