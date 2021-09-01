---
layout: post
title: CISSP Study Notes Chapter 21 - Malicious Code and Application Attacks
date: 2021-09-01 07:30
author: thmsrynr
comments: true
categories: [cissp, security, certifications]
---
Chapter 21 covers the topics of assessing vulnerabilities of security designs and vulnerabilities in web based systems, as well as identifying security controls in development environments and applying secure coding guidelines.

Last summer I spent about a month studying for and getting my Certified Information Systems Security Professional (CISSP) certification from ISC2. I went about studying for the test a few ways:

* I used the PocketPrep app
* I attended a study bootcamp
* I did a bunch of practice tests

And finally...

* I got the ISC2 CISSP official study guide - I read it cover to cover, and highlighted and annotated the entire thing.

[Twitter (@MrThomasRayner)](https://twitter.com/mrthomasrayner) told me there is interest in seeing my study notes. So, here we go! Welcome to my 21 part series on the takeaways and crucial points from each chapter in the ISC2 CISSP official study guide. To be clear, this isn't a replacement for all those other study methods I mentioned above. This is just a supplement. This also isn't *everything* you need to know for the test. This is just what I feel are the most important points.

> It's important to remember that while many of these terms and phrases have different meanings in different contexts, the definitions I'm providing below are the ones that are relevant in the CISSP exam. Your own training or experience may tell you that a definition is incorrect or invalid, but if you want to get the exam questions right, you'll have to know them as they're defined in the books and study material.

The CISSP exam is often said to be "a mile wide but only an inch deep" which means you need to know a little bit about **a lot of stuff**. Accordingly, these posts contain **a lot of points** and while you might not be questioned on all of them, you could be questioned on any of them. It's important to have a good grip on *every chapter* in its entirety.

## Previous Chapters

* [Chapter 1: Security Governance Through Principles and Policies](/cissp-study-notes-ch1)
* [Chapter 2: Personnel Security and Risk Management Concepts](/cissp-study-notes-ch2)
* [Chapter 3: Business Continuity Planning](/cissp-study-notes-ch3)
* [Chapter 4: Laws, Regulations, and Compliance](/cissp-study-notes-ch4)
* [Chapter 5: Protecting Security of Assets](/cissp-study-notes-ch5)
* [Chapter 6: Cryptography and Symmetric Key Algorithms](/cissp-study-notes-ch6)
* [Chapter 7: PKI and Cryptographic Applications](/cissp-study-notes-ch7)
* [Chapter 8: Principles of Security, Models, Design, and Capabilities](/cissp-study-notes-ch8)
* [Chapter 9: Security Vulnerabilities, Threats, and Countermeasures](/cissp-study-notes-ch9)
* [Chapter 10: Physical Security Requirements](/cissp-study-notes-ch10)
* [Chapter 11: Secure Network Architecture and Securing Network Components](/cissp-study-notes-ch11)
* [Chapter 12: Secure Communications and Network Attacks](/cissp-study-notes-ch12)
* [Chapter 13: Managing Identity and Authentication](/cissp-study-notes-ch13)
* [Chapter 14: Controlling and Monitoring Access](/cissp-study-notes-ch14)
* [Chapter 15: Security Assessment and Testing](/cissp-study-notes-ch15)
* [Chapter 16: Managing Security Operations](/cissp-study-notes-ch16)
* [Chapter 17: Preventing and Responding to Incidents](/cissp-study-notes-ch17)
* [Chapter 18: Disaster Recovery Planning](/cissp-study-notes-ch18)
* [Chapter 19: Investigations and Ethics](/cissp-study-notes-ch19)
* [Chapter 20: Software Devlopment Security](/cissp-study-notes-ch20)

## Chapter 21 - Malicious Code and Application Attacks

### My key takeaways and crucial points

#### Malicious Code

* Script kiddie - malicious individual who doesn't understand the technology behind vulnerabilities, but downloads and launches ready to use tools. Often located in countries with weak law enforcement, use malware to steal money and identities.
* Advanced persistent threat - APT, sophisticated adversaries with advanced technical skills and financial resources. Often military units or intelligence agencies, and have access to zero day exploits.
* Virus - two main functions, propagation and destruction
  * Propagation techniques
    * Master boot record - attack bootable media
    * File infector - ending in .exe or .com, alter code of executables
    * Macro - leverage scripting functionality of other software
    * Service injection - inject into trusted runtimes like explorer.exe
* Antivirus mechanisms
  * Signature based detection - database of characteristics that indentify viruses
  * Eradicate virues
  * Quarantine - isolate but not remove
  * Require frequent updates
  * Heuristic - examines the behavior of software to look for bad behavior
* Multipartite virus - uses more than one propagation technique
* Stealth virus - tampers witht he OS to fool antivirus into thinking everything is fine
* Polymorphic virus - modifies their own code from system to system
* Encrypted virus - similar to polymorphic
* Hoax - nuisance and wasted resources
* Logic bomb - lies dormant until triggered by one or more met conditions like time, a program launch, etc.
* Trojan horse - software that appears benevolent but carries a malicious payload
* Ransomware - encrypts files and demands payment in exchange for the decryption key
* Worms - propagates themselves without requiring human intervention
* Code red worm - summer of 2001, attached unpatched Microsoft IIS servers
* Stuxnet - mid 2010, attached unprotected administrative shares and used zero day vulnerabilities to specifically attach systems used in the production of material for nuclear weapons
* Spyware - monitors your actions
* Adware - shows you advertisements
* Zero day attack - the necessary delay between discovery of a new type of malicious code and the isuance of patches creates a window for zero day attacks

#### Password Attacks

* Passowrd guessing - attackers simply attempt to guess the user's password
* Dictionary attacks - tools like John the Ripper take a list of possible passowrds and run an encryption function against them to see which one matches an encrypted password
* Rainbow table - pre-calculated list of known plaintext and its encrypted value, used to decrease time taken to do dictionary attacks
* Social engineering
  * Tricking a user into sharing sensitive information like their password
  * Spear phishing - specifically targetted at an individual
  * Whaling - subset of spear phishing sent to high value targets
  * Vishing - phishing over voice communications
  * Dumpster diving - attackers go through trash to look for sensitive informati9on
* Users should choose strong passwords and keep them a secret

#### Application Attacks

* Buffer overflows - devs don't properly validate user input, and input that is too large can overflow a data structure to affect other data stored in memory.
* Time of check/time of use - timing vulnerability where a program checks access permissions to far in advance of a resource request
* Back door - undocumented sequences that allow individuals to bypass normal access restrictions

#### Web Application Security

* Cross site scripting - XSS, when web apps contain some kind of reflected input. User input is embedded in the site and can be used to perform malicious activities.
* Cross site request forgery - XSRF/CSRF, similar to cross site scripting, but exploit a trust relationship. Exploit the trust a remote site has in a user's system to execute commands on the user's behalf, often when users are logged into multiple websites at the same time in one browser window.
* SQL injection - poorly santitized input contains SQL commands which are executed. Combat by using prepared statements, validating user input, and limiting account privileges.

#### Reconnaissance Attacks

* Reconnaissance - Attackers find weak points in targets to attack.
* IP probes - automated tools that attempt to ping addresses in a range.
* Port scans - probe all the active systems on a network and determine what services are running on each machine.
* Vulnerability scans - discovery specific vulnerabilities in a system.

#### Masquerading Attacks

* Impersonation of someone who does not have the appropriate access permissions.
* IP spoofing - an attacker reconfigures their system to make it look like they haev an IP address of a trusted system.
* Session hijacking - an attacker intercepts part of the commmunication between an authorized user and a resource, and then uses a hijacking technique to take it over and assume the identity of the authorized user.
