---
layout: post
title: What's the difference between -split and .split() in PowerShell?
date: 2017-10-11 07:00
author: thmsrynr@outlook.com
comments: true
categories: [-split, beginner series, beginner series, PowerShell, powershell, splitting strings, string manipulation, string manipulation]
---
Here's a question I see over and over and over again: "I have a string and I'm trying to split it on this part, but it's jumbling it into a big mess. What's going on?" Well, there's splitting a string in PowerShell, and then there's <em>splitting a string in PowerShell</em>. Confused? Let me explain.

<!--more-->

Say you have this string for our example.

<pre class="lang:ps decode:true ">PS&gt; $splitstring = 'this is an interesting string with the letters s and t all over the place'</pre>

Now let's say you want to split it on all the "s" characters. You might do this and get these results.

<pre class="lang:ps decode:true ">PS&gt; $splitstring.split('s')

thi
 i
 an intere
ting
tring with the letter

 and t all over the place</pre>

That did exactly what we thought it would. It took our string and broke it apart on all the "s"'s. Now, what if I want to split it where there's an "st"? There's only two spots it should split: the "st" in "intere<strong>st</strong>ing" and in "<strong>st</strong>ring". Let's try the same thing we tried before.

<pre class="lang:ps decode:true ">PS&gt; $splitstring.split('st')


hi
 i
 an in
ere

ing

ring wi
h
he le

er

 and
 all over
he place</pre>

Well that ain't right. What happened? If we look closely, we can see that our string was split anywhere that there was an "s" or a "t", rather than where there was an "st" together.

.split() is a method that takes an array of characters and then splits the string anywhere it sees any of those characters.

-split is an operator that takes a pattern string (regular expression) and splits the string anywhere it sees that pattern.

Here's what I should have done to split our string anywhere there's an "st".

<pre class="lang:ps decode:true ">PS&gt; $splitstring -split 'st'

this is an intere
ing
ring with the letters s and t all over the place</pre>

That looks more like we're expecting.

Remember, .split() takes an array of characters, -split takes a string.
