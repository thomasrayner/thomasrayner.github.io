---
layout: post
title: Learn PowerShell With PSKoans
date: 2018-11-14
author: thmsrynr
comments: true
categories: [learning, PowerShell, powershell]
---
If you've found your way to this blog, you probably already have a reasonable understanding of basic PowerShell concepts (or maybe that's a foolish assumption). But, how about all your coworkers? And for you, you're probably not done learning yet. There are plenty of ways to learn PowerShell - books, online courses, stealing code from blogs - but in my opinion, the best way to learn PowerShell is by writing PowerShell.

Normally, "learning by doing" when it comes to PowerShell involves just writing scripts and modules to satisfy the requirements of your job or side project. This is great, but you'll end up not exploring certain areas of the language, and sometimes it's nice to be able to know how to do your job before you need to start doing it... so let me introduce you to PSKoans.

<!--more-->

<a href="https://github.com/vexx32/PSKoans" target="_blank" rel="noopener">PSKoans</a> is a PowerShell module written Joel Sallow, with the purpose of helping people learn PowerShell. The readme.md on his GitHub page for PSKoans does a good job of explaining what's going on, and how to use the tool, so I'm not just going to reproduce that. Instead, I'm just going to share my initial thoughts and experience.

Like me, Joel is active in the PowerShell Slack/Discord/IRC channel where people often come to get help with - you guessed it - PowerShell. After seeing stuff about PSKoans discussed for a while, and as I realized that I needed to come up with a good way to help my team at work improve their PowerShell chops, I figured I should give it a try and see if PSKoans would be suitable for use within my team.

Between a few interruptions, it took me a couple hours to work my way through the Foundations set of koans, which cover basics such as working with collections, looping, different operators, and conditionals. In my opinion, it's a pretty darn complete set of foundations. The files you work through themselves are, for the most part, really clear about what you need to be doing, and what you should be learning. If there's any spots that aren't clear, clarity was soon restored by looking at the output of <code>measure-karma</code> which is an included function for tracking your progress There was one particular spot where I stumbled upon a koan that wasn't quite right, so I opened <a href="https://github.com/vexx32/PSKoans/issues/81" target="_blank" rel="noopener">an issue for it</a>, and Joel fixed it the same day. Now that's service.

I'm going to go ahead and use PSKoans with my team as a practical learning tool. Some people prefer books or online courses, and that's awesome. There's plenty of those already. What is awesome to see is people like Joel giving back to the community by making learning systems like PSKoans that take another approach and offer a hands-on learning that doesn't have to take place in your production environments.

<hr />

<em>Full disclosure: I've only made my way through the foundations, since I don't want to get too far ahead of my team (we might work through some in a workshop setting). Foundations make up more than half the points available at the time of this writing, so it's possible that more sophisticated subjects could use some more coverage. Joel's committed to adding more koans, though, so it's worth watching this active project.</em>
