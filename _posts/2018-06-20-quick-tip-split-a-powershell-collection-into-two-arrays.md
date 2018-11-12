---
layout: post
title: Quick Tip - Split A PowerShell Collection Into Two Arrays
date: 2018-06-20 07:30
author: thmsrynr
comments: true
categories: [beginner series, collections, New Stuff, PowerShell, powershell, PowerShell 5.0, quick tips]
---
Did you know that you can use <strong>Where-Object</strong> to split a collection into two arrays? Like, if you had an array containing the numbers 1 to 10, you could split it into one array of even numbers, and another array of odd numbers? It's pretty cool. Thanks <a href="https://twitter.com/herbm" target="_blank" rel="noopener">Herb Meyerowitz</a> for this tip!

<!--more--><img class="alignnone size-full wp-image-770" src="/wp-content/uploads/2018/06/2018-06-07-07_27_11-Blog-post-topics-OneNote.png" alt="" width="626" height="332" />

As you can tell from Herb's comment in this screenshot, it's actually the .where() method that is relatively new that we're using to split collections this way. The syntax is kind of atypical, so let's break it down.
<pre class="lang:default decode:true">$a, $b = (1..5).where({$_ % 2}, 'split')</pre>
<ul>
 	<li><strong>$a, $b = </strong>
<ul>
 	<li>This part is creating two variables, named a and b that will be used to contain the output of our splitting activity.</li>
</ul>
</li>
 	<li><strong>(1..5)</strong>
<ul>
 	<li>This just creates an array of the numbers 1 through 5.</li>
</ul>
</li>
 	<li><strong>.where( )</strong>
<ul>
 	<li>This is a method that comes with PowerShell 5 (I'm pretty sure) which works mostly like the <strong>Where-Object</strong> cmdlet that you're used to. Most people just use it to filter collections on a filterscript (stay tuned) but it also takes other arguments.</li>
</ul>
</li>
 	<li><strong>{$_ % 2}</strong>
<ul>
 	<li>This is the filterscript, or basically the criteria we're using to split up our collection. It will effectively create a true and a false list like the condition in an if statement. The percent sign is the modulus operator and will determine if the number is divisible by two without a remainder or not.</li>
</ul>
</li>
 	<li><strong>'split'</strong>
<ul>
 	<li>This is the mode. By default, the collection is filtered using the filterscript like when using <strong>Where-Object </strong>and only the objects matching the condition are returned. But that's not the only mode! We're going to use the <em>split</em> mode to break it into two collections. Maybe another blog post will come out on some of the other modes.</li>
</ul>
</li>
</ul>
That's it!
