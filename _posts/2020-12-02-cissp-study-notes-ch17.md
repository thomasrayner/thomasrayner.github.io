---
layout: post
title: CISSP Study Notes Chapter 17 - Preventing and Responding to Incidents
date: 2020-12-02 07:30
author: thmsrynr
comments: true
categories: [cissp, security, certifications]
---
Chapter 17 goes over conducting logging and monitoring activities, conducting incident management, and operating and maintaining detective and preventative measures.

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

## Chapter 16: Managing Security Operations

### My key takeaways and crucial points

#### Managing Incident Response

* Defining an incident
  * Any event that has a negative effect ont he confidentiality, integrity or availability of an organization's assets
  * ITIL says it's any unplanned interruption
  * A computer secuirty incident is a result of an attack, or the result of malicious or itentional actions on the part of users
  * NIST 800-61
* Incident response steps
  * Incident response is an ongoing activity
  * Does not include a counterattack
    * Usually illegal, often results in escalation
* Detection
  * Must be able to quickly identify false alarms and user errors
* Response
  * Computer incident response team (CIRT)
  * Activate the team during a major security incident, but not for minor incidents
  * Computers should not be turned off when containing an incident
    * Important for forensics
* Mitigation
  * Contain an incident
  * Limit the effect or scope of an incident
  * Address it without worrying about it spreading
* Reporting
  * Within the org and to groups outside the org
  * Beware of legal requirementse
  * If a data breach exposes PII, the organization must report it
  * Consider reporting the incident to official agencies, they might be able to help
* Recovery
  * Recover the syustem or return it to a fully functioning state
  * Restoring data
  * Ensure it is configured properly and is at least as secure as it was before the incident
  * Configuration management and chanage management programs are important here
* Remediation
  * Attempt to identify what allowed it to occur, implement methods to prevent it from happening again
  * Root cause analysis
* Lessons learned
  * Examine the incident and the response to see if there are any lessons to be learned
  * Improve the response
  * Output of this stage can be fed back to the detection stage
  * Create a report

#### Implementing Detective and Preventive Measures

* Basic preventive measures
  * Keep systems and applications up to date
  * Remove or disable unneeded services and protocols
  * Use intrusion detection and prevention syustems
  * Use up to date anti-malware software
  * Use firewalls
  * Implement configuraiton and system management processes

#### Understanding Attacks

* Botnets
  * Bot herder
    * A criminal who controls computers in the botnet via one or more command and control servers
  * Defense in depth
  * Educating users
* Denial of service attacks
  * DoS attacks
  * Prevent a system from processing or responding to legitimate traffic or requests for resources and objects
  * Distributed denial of service attacks occur when multiple systems attack a single system at the same time
  * Distributed reflective denial of service attack doesn't attack the victim directly but manipulates traffic or a service so the attacks are reflected back to the victim from other sources
* SYN flood attack
  * Disrupts the standard 3 way handshake used by TCP
  * Consume available memory and processing power
  * SYN cookies can block this attack
  * Reduce the amoun tof time a server will wait for an ACK
* Smurf attacks
  * Another type of flood attack, but floods with ICMP echo packets instead of TCP SYN
* Fraggle attacks
  * Similar to smurf, but instead of ICMP, useds UDP packets over ports 7 and 19
* Ping flood
  * Floods a victim with ping requests
* Ping of death
  * Oversized ping packet
  * Buffer overflow error
* Teardrop
  * Attacker fragments traffic in a way that a system is unable to put it back together
* Land attacks
  * Attacker sends spoofed SYN packets to a victim using the victim's IP address as botht he soure and destination IP
* Zero day exploit
  * Vulnerabilities that are unknown to others
  * The attacker is the only one aware of the vulnerability, before the vendor makes a patch
  * The gap between when the vendor releases the patch and when administrators apply it is a dangerous zone
  * Honeypots and padded cells
* Malicious code
  * Any script or program that performs an unwanted, unauthorized or unknown activity on a computer system
  * Drive by downloads
    * Code is installed on a user's system without the user's knowledge
* Man in the middle attacks
  * MITM
  * Malicious users gain a position logically between the two endpoints
  * Copying or sniffing the traffic between parties
  * A store and forward or proxy mechanism
  * Intrusion detection systems cannot usually detect MITM or hijack attacks
  * VPNs
* Sabatoge
  * A criminal act of destruciton or disruption committed against an organization by an employee
  * Employee terminations should be handled swiftly
    * Account access should be disabled ASAP
* Espionage
  * The malicious act of gathering classified information about an organization
  * Disclosing or selling ifnormation to a competitor
  * Mole/plant - an employee with a secret allegience to another organization whose goal is to steal information
  * Screen and track employees effectively

#### Intrusion Detection and Prevention Systems

* Intrusion
  * Attacker can bypass security mechanisms
* Intrusion detection
  * Monitors recorded information
* Intrusion prevention system
  * IPS
  * Can take steps to stop/prevent intrusions
  * NIST 800-96
* Knowledge/Behavior-based detection
  * Knowledge based
    * aka signature based
    * Database of known attacks
  * Behavior based
    * aka statistical/anomaly, heuristics
    * Creates a baseline of normal activities and events on a system, detects abnormal activity
    * aka an Expert System
* SIEM systems
  * Security ifnromation and event management system
  * Advanced analytic tools
  * Passive response
    * Notifies administrators
  * Active response
    * Can modify the environment
      * Modifies ACLs, addresses, disable communications over specific segments, etc.
* Host and Network based IDSs
  * Host based
    * Monitors a single computer
    * Can detect anomalies on the host that a network IDS cannot
    * Requires admin attention on each system
  * Network based
    * Evaluates network activity
    * Can monitor a large network to collect data at key locations
    * Switches are often used as a preventive measure against rogue sniffers
    * Very little effect on network performance
    * Usually able to detect initation of attack, not always about the success of an attack
* Intrusion prevention systems
  * Placed in line with traffic
  * Active IDS that is not placed in line can check the activity only after it has reached the target

#### Specific Preventive Measures

* Honeypot
  * Individual computers created as a trap for intruders
  * Honeynet, a network of honeypots
  * Do not host any data of real value
  * Opportunity to observe an attacker's activity
  * Enticement vs entrapment
    * Intruder must discover it through no outward effort of the honeypot owner
  * Psuedo flaws
    * False vulnerabilities
  * Padded cells
    * Look and feel like an actual network but attackers are unable to perform any malicious activities
    * Offer fake data
* Warning banners
  * Inform users and iuntruders about security policy guidelines
  * Legally bind uesrs
  * No tresassing signs
* Anti-malware
  * Signature files and heuristic capabilities must be kept up to date
  * Firewalls with content-filtering capabilities
  * Install only one anti-malware applicatoin on any system
  * Least privilege helps
  * Educating users
* Whitelisting and blacklisting
  * Should be called allowlisting and denylisting, but these are the terms CISSP uses
  * Whitelisting identifies a list of applicaitons that are authorized to run
  * Blacklisting is a list of applications that are blocked
* Firewalls
  * Filtering traffic based on IP address, port, protocols
  * Second generation firewalls add additional filtering capabilities based on application requirements
  * Next generation firewalls function as a unified threat management device and have even more filtering, like packet filtering and stateful inspection, as well as packet inspeciton
* Sandboxing
  * Prevents the application from interacting with other applciations
  * Virtualization techniques
* Third party security services
  * SaaS
    * Software as a service
* Penetration testing
  * Mimics an actual attack to attempt to identify which techniques attackers cna use to circumvent security
  * NIST 800-115
  * Include a vulnerability scan/assessment
  * Attempt to exploit weaknesses
  * Determine how well a system can tolerate attack
  * Identify employees' ability to detect and respond to attacks in real time
  * Identify additional controls that can be implemented to reduce risk
  * Pentesting risks
    * Some methods can cause outages
    * Should stop before doing actual damage
    * Should try to perform pentesting in a test system
  * Must always have permission in writing with the risks spelled out
  * Black box testing
    * Zero knowledge
  * White box testing
    * Full knowledge
  * Gray box testing
    * Partial knowledge
  * Social engineering techniques are often used
  * Must protect pentesting reports because they describe attacks against the system
  * Reports must make a recommendation
  * AKA ethical hacking

#### Logging, Monitoring, and Auditing

* Logging
  * Recording information about events to a file or database
* Log types
  * Security logs - access to resources
  * System logs - system events
  * Application logs - specific applications
  * Firewall logs
  * Proxy logs - include details such as what sites specific users visit and how much time they spend on those sites
  * Change logs
    * Part of a disaster recovery program
* Protecting log data
  * Use logs to recreate events leading up to and during an incident only if the logs haven't been modified
  * Store copies on a central system like a SIEM
  * FIPS 200
* Audit trails
  * Records created when information about events is stored in one or more databases or log files
  * Passive form of detective security control
  * Also serve as a deterrent
  * Essential as evidence in the prosecution of criminals
* Monitoring and accountability
  * Users claim an identity and must prove their identity by authenticating
  * Audit trails record their activity
  * Users who are aware that lgos are recording are less likely to try to circumvent security controls or perform unauthorized activities
* Monitoring
  * The process of reviewing logs looking for something specific
  * Continuous process
  * Log analysis
    * Detailed form of monitoring, logs are analyzed for trends and patterns
  * Many orgs use a centralized application for monitoring
  * SIEMs may include a correlation engine to help combine multiple log sources into meaningful data
* Sampling
  * Extracting elements from a large collection to construct a meaningful representation of the whole
* Clipping levels
  * Predefine dthreshold for the event, ignoring events until they reach the level
* Keystroke monitoring
  * Act of recording keystrokes a user performs on a keyboard
  * Often compared to wiretapping
* Traffic and trend analysis
  * Examine the flow of packets rather than the contents
* Egress monitoring
  * Watching outgoing traffic to prevent data exfiltration
* Data loss prevention
  * Detect and block data exfiltration attempts
  * Network based scan all outgoing data
  * Endpoint based scan files stored on a system
  * Deep level examinations of data in files
* Steganography
  * The practice of embedding a message within a file
* Watermarking
  * The practice of embedding an image or pattern in paper that isn't readily perceivable, often to thwart counterfeiting attempts

#### Auditing to Assess Effectiveness

* Auditing
  * A methodical examination of an environment
  * Use audit logs and monitoring tools to track activity
  * Auditing - Inspection or evaluation
* Auditors
  * Test and verify that processes and procedures are in place to implement security policies or regulations
* Inspection audits
  * Clearly define and adhere to the frequence of audit reviews
* Access review audits
  * Ensure that object access and account management practices suppor the current security policy
  * Ensure that accounts are disabled and deleted in accordance with best practices and security policies
  * Typical termination process:
    * At least one witness is present during exit interview
    * Account access terminated during interview
    * Employee ID badges and physical credentials are collected
    * Employee escorted off premises immediately
* User entitlement audits
  * Refers to the prvileges gratned to users
  * Enforce least privilege principle
* Audits of privileged groups
  * High level adminstrator groups
  * Dual administrator accounts
    * Separation of privileges (normal account and a privileged account)
* Security audits and reviews
  * Patch management - patches are evaluated ASAP, properly deployed through a testing process
  * Vulnerability management - compliance with established guidelines, scans and assessments
  * Configuration management - Use tools to check specific configurations of systems and identify when a change has occured
  * Change management - Changes are implemented in accordance to change management policy
* Reporting audit results
  * Report needs purpose, scope and results
* Protecting audit results
  * Contain sensitive information, need a classification label
  * Sometimes create a seaprate audit report with limited data for separate distribution
  * When distributing, get signed confirmation
* External auditors
  * Some laws require this
  * Provide a level of objectivity that interal audits can't
  * Interim reports - written or verbal given to the org about observerations that demand immediate attention
