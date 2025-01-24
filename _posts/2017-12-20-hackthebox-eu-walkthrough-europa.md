---
layout: post
title: HackTheBox.eu Walkthrough - Europa
date: 2017-12-20 07:00
author: thmsrynr@outlook.com
comments: true
categories: [bash, ethical hacking, europa, hacking, hackthebox, hackthebox, hackthebox.eu, htb, linux, penetration testing, pentesting, pentesting, red team, security, something different, something different]
---
If you're a frequent reader of my blog, you know that I mostly post about PowerShell, Microsoft related automation, and that sort of thing. In a previous life, however, I thought I wanted to make a career out of infosec - particularly penetration testing and red team type of stuff. I'm super happy with where my career went instead, but from time to time, I enjoy attempting to knock some of the rust off my ethical hacking/pentesting skills (what little of them there are), and trying my hand at some vulnerable by design boxes. Since it's the holiday season, I decided to switch things up a little bit for the next couple blog posts.

HackTheBox.eu offers a cool variety of vulnerable by design virtual machines for people to practice their pentesting skills against. There are strict rules about sharing spoilers for "active" boxes, but there are only so many of those, and lots of "retired" boxes are available as well. In today's post I'm going to share a walkthrough of how I did the retired box "Europa".

<!--more-->

I am not a professional penetration tester or red teamer, nor is this meant to be the type of write up that I'd provide to a client if I was doing this for money. This is just a summary of what I did to get the user and root flags on the box. I'm not going to get into any of the rabbit holes or areas that didn't lead to a solution<strong> (because this isn't a real write up)</strong>.

First things first, I ran <em>nmap</em> to see what might be up and running on the box. I ran safe scripts, enumerated versions, and saved all output with the file basename "nmap".
```
nmap -sC -sV -oA nmap 10.10.10.22
```
Among other things, one of the items that is immediately revealed is that Europa is running a web server, and has an SSL certificate protecting the HTTPS part. Right there in the <em>nmap</em> output, you can see that the certificate has a subject alternative name for an "admin-portal" subdomain.

Obviously with a name as juicy as "admin-portal", that's where I'm going to start. You can find the login.php page there. As with any login form, I tried a couple manual SQL injection techniques but wasn't immediately granted access, so I used Burpsuite to capture a post request to login.php and sent it over to <em>sqlmap</em>. Eventually <em>sqlmap</em> will pop that login form open for you and get you redirected to dashboard.php.

Poking around the admin portal, you'll quickly find a page named tools.php that has a "VPN config builder". It appears to be doing some sort of find and replace to plug in a value that you provide. Immediately, this seems like a place to insert some code.

Capture one of the posts to the config builder and you'll see that there are actually a few variables being sent. One for the pattern being detected (where the "IP" will be inserted), the IP/value that will be inserted into the config, and a base for the config itself (which includes the pattern in the first variable. PHP uses a function called <em>preg_replace</em> to do this kind of find and replace functionality, and doesn't execute code by default. There is, however, a way to make it do just that.

If you replace the IP address to be inserted into the config with bash code, it will take the literal bash code that you entered and write that out without executing it. If you append an "e" to the first argument that <em>preg_replace</em> takes, though, then it will evaluate the bash code and replace your pattern with the value. So if you change the pattern to "/mything/e", the value to replace it with (variable named IP) to some bash code, and then the rest of the config to just be "mything", that will make it easier to comb through the output. This can all be done in Burpsuite repeater, and you'll see the output of the bash command you put in the IP field instead of the literal string that you put in there. You can use this technique to get the user flag and to create a reverse shell.

If you run any decent privilege escalation enumeration script after you're logged in with your reverse shell (I prefer LinEnum.sh but I'm a noob so do what you like), you'll see that there is an unusual PHP file being executed by root via cron every minute. You can read it and see that it clears logs and then calls another script when it's done. This second script that it calls is world writable, so you can put anything you want in it, and it will be executed as root in about a minute. You can use this technique to get the root flag, and you're done.

Overall, I enjoyed this box. I learned about the <em>preg_replace</em> attack vector which I didn't previously know about, and I like learning new things. The privesc was really straight forward, but sometimes that's not so bad.
