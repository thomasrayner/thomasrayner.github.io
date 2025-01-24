---
layout: post
title: CISSP Study Notes Chapter 14 - Controlling and Monitoring Access
date: 2020-10-06 07:30
author: thmsrynr
comments: true
categories: [cissp, security, certifications]
---
Chapter 14 is about identity and access management (IAM), and discusses all kinds of different access control: role based, rule based, mandatory,discretionary, and attribute based.

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

## Chapter 14: Controlling and Monitoring Access

### My key takeaways and crucial points

#### Comparing Permissions, Rights, and Privileges

* Permissions
  * The access granted for an object and what you can do with it
* Rights
  * The ability to take an action on an object
* Privileges
  * The combination of rights and permissions

#### Understanding Authorization Mechanisms

* Implicit deny
  * Access to an object is denied unless it has been explicitly granted
* Access control matrix
  * A table that includes subjects, objects, and assigned privileges
* Capability tables
  * Like an ACL, but focused on subjects
* Constrained interface
  * Restricted interfaces that control what users can do or see based on their privileges
* Content depended control
  * Restrict access to data based on the content within an object
  * Ex: A database view
  * "What" data is being accessed
* Context depended control
  * Require specific activity before granting access
  * Ex: Date and time bound access
  * "How" you're accessing data
* Need to know
  * Granted access only to what you *need to know* to perform your job
* Least privilege
  * Subjects are granted only the privileges they need to perform their work tasks and job functions
  * Will also include rights to take action on a system
* Separation of duties and responsibilities
  * Sensitive functions are split into tasks performed by two or more employees

#### Defining Requirements with a Security Policy

* Security policy
  * A document that defines the security requirements for an organization
* Senior leadership approves the security policy

#### Implementing Defense in Depth

* Defense in depth
  * Multiple layers or levels of access controls to provide layered security
* Key components
  * Security policy
  * Personnel, training
  * Combination of administrative, technical, and physical access controls

#### Summarizing Access Control Models

* Discretionary access control
  * Every object has an owner who can grant or deny access to any other subjects
* Role based access control
  * User accounts are placed in roles and administrators assign privileges to the roles
* Rule based access control
  * Global rules apply to all subjects
  * AKA restrictions/filters
* Attribute based access control
  * Uses rules that can include multiple attributes
  * More flexible than rule based access control
  * Plain language statements
* Mandatory access control
  * Labels applied to both subjects and objects

#### Discretionary Access Control

* Allows owner/creator/data custodia of an object to control and define access to the object
* Using access control lists (ACLs)

#### Nondiscretionary Access Control

* Administrators centrally administer access controls and can make changes that affect the entire environment

#### Role Based Access Control

* AKA task-based access control
* AKA RBAC
* Privilege creep
  * Users accrue privileges over time as their roles and access needs change
* Administrators identify roles/groups by work function
* Useful in dynamic environments with frequent personnel changes

#### Rule Based Access Control

* Rules, restrictions, filters determine what can and cannot occur on a system
* Global rules apply to all subjects
* RBAC refers to *ROLE* based access control
* Firewalls include a set of rules within an ACL
* Implicit deny

#### Attribute Based Access Control

* ABAC
* Uses policies that include multiple attributes for rules
* Can be any characteristic of users, network, devices

#### Mandatory Access Control

* MAC
* Uses classification labels
* Security domain
  * A collection of subjects and objects that share a common security policy
* Often referred to as a lattice-based model
* Compartmentalization enforces need to know principle
* Hierarchical environment
  * Ordered structure from low security to medium security to high security
  * Classification labels
* Compartmentalized environment
  * No relationship between one security domain and another
* Hybrid environment
  * Combines both hierarchical and compartmentalized concepts

#### Understanding Access Control Attacks

* Risk elements
  * Threat
    * A potential occurrence that can result in an undesirable outcome
  * Vulnerability
    * Any type of weakness
  * Risk management
    * Attempting to reduce or eliminate vulnerabilities, or reduce the impact of potential threats by implementing controls or countermeasures
    * Process
      * Identify assets
        * Asset valuation - identifying the actual value of an asset so you may prioritize them
      * Identify threats
        * Threat modeling - identifying, understanding and categorizing potential threats
      * Identify vulnerabilities
* Advanced persistent threats
  * APTs
  * Attackers who are working together, highly motivated, skilled, and patient
  * Advanced knowledge
* Threat modeling approaches
  * Focused on assets
    * Identify threats to valuable assets
  * Focused on attackers
    * Based on attackers goals
  * Focused on software
    * Based on potential threats against software
* Identifying vulnerabilities
  * Identifying strengths and weaknesses of different access control mechanisms

#### Common Access Control Attacks

* Access aggregation attacks
  * Collecting multiple pieces of non-sensitive information and combining them to learn sensitive information
  * Reconnaissance
* Password attacks
  * Passwords are the weakest form of authentication
  * Dictionary attack
    * Attempt to discover passwords by using every possible password in a predefined database or list of common or expected passwords
  * Brute force attack
    * Attempt to discover passwords for accounts by systematically attempting all possible combinations of letters, numbers and symbols
    * Hybrid attack attempts a dictionary attack and then a brute force
  * Birthday attack
    * Focuses on finding collisions
    * The birthday paradox states that if there are 23 people in a room, there is a 50% chance that two of them will have the same birthday (month and day only, not year)
  * Rainbow table attack
    * Rainbow tables are large databases of precomputed hashes
    * Salt passwords to reduce effectiveness of rainbow tables
      * Salt is random bits added to a password before hashing it, stored in the same database holding the hashed password
      * Pepper is a large constant number stored elsewhere
  * Sniffer attacks
    * Capture packets sent over a network to analyze them
    * AKA snooping attack
    * Wireshark is a popular tool for this
    * Make sure you
      * Encrypt all sensitive data
      * Use one time passwords
      * Implement physical security
      * Monitor the network for signatures from sniffers
* Spoofing attacks
  * AKA masquerading
  * Pretending to be something else
  * Email spoofing
    * Spoofing the email address in the from field of an email
    * Phishing
  * Phone number spoofing
    * Caller ID
    * VoIP
* Social engineering attacks
  * Gaining the trust of someone using deceit to get them to betray organizational security
  * Shoulder surfing is also considered social engineering
    * Looking at someone's screen while they access information
    * Use screen filters
  * Phishing
    * Getting users to open an attachment, click a link, or reply with personal information
    * Drive by downloads
      * Malware that installs itself without the user's knowledge when the user visits a website
    * Spear phishing
      * Phishing where specific users or groups are targeted
    * Whaling
      * Senior or high level executives are targeted
    * Vishing
      * Phishing with a phone system or VoIP
* Smartcard attacks
  * Side channel attack
    * Passive, non-invasive attack that observes how the device functions

#### Summary of Protection Methods

* Control physical access to systems
  * If attackers can gain physical access to a server, they can steal it and do anything to it
* Control electronic access to files
* Create a strong password policy
* Hash and salt passwords
* Use password masking, never display cleartext passwords
* Deploy multifactor authentication
* Use account lockout controls
  * Lock an account after the incorrect password is entered a predefined number of times
  * Implement extensive logging
* Use last logon notification
  * Display information about the last time an account was successfully logged into
* Educate users about security
