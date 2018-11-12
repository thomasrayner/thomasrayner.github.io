---
layout: post
title: HackTheBox.eu Walkthrough - Apocalyst
date: 2018-01-03 07:00
author: thmsrynr@outlook.com
comments: true
categories: [bash, ethical hacking, europa, hacking, hackthebox, hackthebox, hackthebox.eu, htb, linux, penetration testing, pentesting, red team, security, something different, something different]
---
If you're a frequent reader of my blog, you know that I mostly post about PowerShell, Microsoft related automation, and that sort of thing. In a previous life, however, I thought I wanted to make a career out of infosec - particularly penetration testing and red team type of stuff. I'm super happy with where my career went instead, but from time to time, I enjoy attempting to knock some of the rust off my ethical hacking/pentesting skills (what little of them there are), and trying my hand at some vulnerable by design boxes. Since it's the holiday season, I decided to switch things up a little bit for the last couple blog posts.

HackTheBox.eu offers a cool variety of vulnerable by design virtual machines for people to practice their pentesting skills against. There are strict rules about sharing spoilers for "active" boxes, but there are only so many of those, and lots of "retired" boxes are available as well. In today's post I'm going to share a walkthrough of how I did the retired box "Apocalyst".

<!--more-->

I am not a professional penetration tester or red teamer, nor is this meant to be the type of write up that I'd provide to a client if I was doing this for money. This is just a summary of what I did to get the user and root flags on the box. I'm not going to get into any of the rabbit holes or areas that didn't lead to a solution<strong> (because this isn't a real write up)</strong>.

First things first, I ran <em>nmap</em> to see what might be up and running on the box. I ran safe scripts, enumerated versions, and saved all output with the file basename "nmap".
```
nmap -sC -sV -oA nmap 10.10.10.46\n```
You'll quickly find a Wordpress site is up and running. If you run <em>wpscan --enumerate u</em> or just look around at some of the posts, you'll find a username: falaraki. If you use <em>dirbuster</em> and any of the normal wordlists, you may have a challenging time. I used <em>cewl</em> to make a wordlist for <em>dirbuster</em> after receiving a small nudge in the HTB Slack channel. You'll find a whole pile of directories, each one containing a seemingly identical image. Sounds like we're in for everybody's favorite thing in the world: steganography!

I wrote a quick script to download all of them because I love taking up tons of diskspace on my VM, and you'll find that the image in the "Rightiousness" directory looks the same as the others but has a larger file size. You can use <em>steghide extract -sf rightiousness.jpg</em> with no password to extract a wordlist hidden in the larger image. Maybe this is why the box is called Apocalyst... apoca... list. Wordlist. Maybe.

I used hydra on the Wordpress login page with the falaraki username I found earlier and the wordlist that came out of the image. The Wordpress password for falaraki is in the list, and I got in. This password does <strong>not</strong> work for the same user or root on SSH. As far as I could tell, the stegoed wordlist doesn't contain any other useful passwords.

I uploaded my own plugin to the Wordpress site, since falaraki is a Wordpress admin, which executed PHP to get the user flag and a reverse shell onto the box as the www-data user.

If you explore /home/falaraki, you'll find a hidden file named ".secret". Check it out, and you'll see pretty quickly that it's a base64 encoded file. Decode it to find a password for falaraki that you can use to SSH into the box, elevating yourself from www-data to falaraki.

After running some privilege escalation enumeration scripts, it quickly became apparent that falaraki has write permissions on /etc/passwd, so I added a uid 0 user with a password that I knew, authenticated as that user, and used my root privileges to get the root flag.

Overall, I didn't love this box. It felt a little too capture-the-flag-y with all the images and then a wordlist being what was hidden via steganography. Still, I learned about some basic stego techniques which I appreciated, and exploiting the ability to upload my own Wordpress plugins.
