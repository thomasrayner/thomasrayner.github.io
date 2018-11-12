---
layout: post
title: Using PowerShell To Split A String Without Losing The Character You Split On
date: 2017-10-18 07:00
author: thmsrynr@outlook.com
comments: true
categories: [beginner series, beginner series, PowerShell, powershell, regex, regex]
---
Last week, I wrote a post on the difference between .split() and -split in PowerShell. This week, we're going to keep splitting strings, but we're going to try to retain the character that we're splitting on. Whether you use .split() or -split, when you split a string, it takes that character and essentially turns it into the separation of the two items on either side of it. But, what if I want to keep that character instead of losing it to the split?

<!--more-->

Well, we're going to have to dabble in regular expressions. Before you run away screaming, as I know some people do when it comes to regex, let me walk you through this and see if you don't mind dipping a toe in these waters.

In our scenario, I've got a filename and I'm going to split it based on the slashes in the path. Normally I'd get something like this.

```
PS&gt; $filename = get-item C:\temp\demo\thing.txt
PS&gt; $filename -split '\\'

C:
temp
demo
thing.txt
```

Notice how I had to split on "&#92;"? I had to escape that backslash. We're regexing already! Also notice that I lost the backslash on which I split the string. Now let's do a tiny bit more regex in our split pattern to retain that backslash.

```
PS&gt; $filename -split '(?=\\)'

C:
\temp
\demo
\thing.txt
```

Look at that, we kept our backslash. How? Well look at the pattern we split on: <strong>(?=&#92;)</strong>. That's what regex calls a "lookahead". It's contained in round brackets and the "?=" part basically means "where the next character is a " and the "&#92;" still means our backslash. So we're splitting the string on the place in the string where the next character is a backslash. we're effectively splitting on the space between characters.

NEAT! Now what if I wanted the backslash to be on the other side? That is, at the end of the string on each line instead of the start of the line after? No worries, regex has you covered there, too.

```
PS&gt; $filename -split '(?&lt;=\\)'

C:\
temp\
demo\
thing.txt
```

This is a "lookbehind". It's the same as a lookahead, except it's looking for a place where the character to the left matches the pattern, instead of the character to the right. A lookbehind is denoted with the "?&lt;=" characters.

There are plenty of resources online about using lookaheads and lookbehinds in regex, but if you're not looking specifically for regex resources, you probably wouldn't have found them. If PowerShell string splitting is what you're after, hopefully you found this interesting.

Regex isn't that scary, right?
