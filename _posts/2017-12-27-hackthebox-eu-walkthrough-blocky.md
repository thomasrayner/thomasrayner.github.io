---
layout: post
title: HackTheBox.eu Walkthrough - Blocky
date: 2017-12-27 07:00
author: thmsrynr@outlook.com
comments: true
categories: [bash, ethical hacking, europa, hacking, hackthebox, hackthebox, hackthebox.eu, htb, penetration testing, pentesting, pentesting, red team, security, something different, something different]
---
If you're a frequent reader of my blog, you know that I mostly post about PowerShell, Microsoft related automation, and that sort of thing. In a previous life, however, I thought I wanted to make a career out of infosec - particularly penetration testing and red team type of stuff. I'm super happy with where my career went instead, but from time to time, I enjoy attempting to knock some of the rust off my ethical hacking/pentesting skills (what little of them there are), and trying my hand at some vulnerable by design boxes. Since it's the holiday season, I decided to switch things up a little bit for the next couple blog posts.

HackTheBox.eu offers a cool variety of vulnerable by design virtual machines for people to practice their pentesting skills against. There are strict rules about sharing spoilers for "active" boxes, but there are only so many of those, and lots of "retired" boxes are available as well. In today's post I'm going to share a walkthrough of how I did the retired box "Blocky".

<!--more-->

I am not a professional penetration tester or red teamer, nor is this meant to be the type of write up that I'd provide to a client if I was doing this for money. This is just a summary of what I did to get the user and root flags on the box. I'm not going to get into any of the rabbit holes or areas that didn't lead to a solution<strong> (because this isn't a real write up)</strong>.

First things first, I ran <em>nmap</em> to see what might be up and running on the box. I ran safe scripts, enumerated versions, and saved all output with the file basename "nmap".
```
nmap -sC -sV -oA nmap 10.10.10.37
```
You'll quickly see that there is a Wordpress site running, and when you visit it, it appears to be a place for information on someone's Minecraft server. After some basic poking around, and taking notice of the "Notch" username of the person who made all the posts on the site, I ran <em>dirbuster</em> on it to find any possibly interesting directories or files.

Poking around in the <em>dirbuster</em> results, I found a /wp-content/uploads folder that contained two .jar files. It was around this time that I learned that .jar files are basically just archives and can be unzipped with things like <em>unzip</em> on the Linux CLI. Predictably, there are some .class files in the extracted data, which can be decompiled using <em>javap</em>.

If you search through the decompiled classes, you'll find a hard coded password for "root". This isn't the root password, but rather is for something Minecraft related. Still, it seemed too good to be true, so I started sticking it other places, using the "Notch" username that was found earlier.

Turns out, password re-use is at play here and you can SSH into Blocky using the "Notch" account and the password from the decompiled .class. Notch can read the user flag.

I spent far too long enumerating and poking around looking for a privilege escalation of some kind, when if you just run <em>sudo -l</em>, you'll see that Notch has full rights, and so you can <em>sudo</em> anything you want, including reading the root flag.

Even though Blocky was a very easy box to pop, I still learned about extracting jars and decompiling classes, which made me appreciate it for what it is. I also learned that there are a few pieces of low-hanging privilege escalation fruit to check on every box before going too nuts enumerating everything.
