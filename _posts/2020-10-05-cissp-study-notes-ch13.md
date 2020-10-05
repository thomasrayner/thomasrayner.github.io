---
layout: post
title: CISSP Study Notes Chapter 13 - Managing Identity and Authentication
date: 2020-10-05 07:30
author: thmsrynr
comments: true
categories: [cissp, security, certifications]
---
Chapter 13 is an important chapter that gets into controlling physical and logical access to assets, managing identification and authentication of people, devices and services, integrating identity as a third-party service, and managing the identity and access provisioning lifecycle.

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

## Chapter 13: Managing Identity and Authentication

### My key takeaways and crucial points

#### Comparing Subjects and Objects

* *Subjects* are active entities that access a passive object
* *Objects* are passive entities that provide information to active subjects

#### The CIA Triad and Access Controls

* Confidentiality
  * When unauthorized entities can access systems or data, it results in a loss of confidentiality
* Integrity
  * Unauthorized changes
* Availability
  * Data should be available to users and other subjects when they are needed

#### Types of Access Control

* Access control includes the following overall steps
  1. Identify and authenticate users or other subjects attempting to access resources
  1. Determine whether the access is authorized
  1. Grant or restrict access based on the subject's identity
  1. Monitor and record access attempts
* Preventive access control
  * Attempts to thwart or stop unwanted or unauthorized activity from occurring
* Detective access control
  * Attempts to discover or detect unwanted or unauthorized activity
* Corrective access control
  * Modifies the environment to return systems to normal after an unwanted or unauthorized activity has occurred
* Deterrent access control
  * Discourages security policy violations
* Recovery access control
  * Repair or restore resources, functions, and capabilities after a security policy violation
* Directive access control
  * Direct, confine, or control the actions of subjects to force or encourage compliance with security policies
* Compensating access control
  * Provides an alternative when it isn't possible to use a primary control
  * Increase the effectiveness of a primary control
* Administrative access control
  * Policies and procedures
* Logical/technical controls
  * Hardware or software mechanisms
* Physical controls
  * Items you can physically touch

#### Comparing Identification and Authentication

* Identification
  * The process of a subject claiming, or professing, an identity
* Authentication
  * Verifying the identity of the subject by comparing one or more factors against a database of valid identities
* Registration
  * When a user is first given an identity
* Authorization
  * Access to objects based on proven identities
  * Indicates who is trusted to perform specific operations
* Accountability
  * Auditing is implemented
  * The process of tracking and recording subject activities within logs
  * Relies on effective identification and authentication, but does not require effective authorization

#### Authentication Factors

* Type 1
  * Something you *know*
  * Ex: password, PIN
* Type 2
  * Something you *have*
  * Ex: token, phone, smartcard
* Type 3
  * Something you *are*
  * Ex: Fingerprint, retina scan
* Context-aware authentication
  * Based on location, time of day, mobile device
  * May implement a geo-fence so resources are only available on some devices if the device is in a specific place
  * Detecting impossible travel
* Passwords
  * Type 1
  * A static password stays the same for a length of time
  * Weakest form of authentication
  * Creating strong passwords
    * Max age
    * Complexity
    * Length
    * History
  * Passphrases are more effective
    * Longer strings of characters made up of multiple words
  * NIST 800-63B suggests comparing a user's password against a list of commonly known simple passwords and rejecting the commonly known passwords
* Cognitive passwords
  * Challenge questions
  * Ex: What is your birth date? What is the name of your first pet?
  * Answers are commonly available on the internet
* Smartcards
  * Type 2
  * Certificates are used for asymmetric crypto like encrypting data or signing email
* Tokens
  * Type 2
  * Password-generating devices
  * Synchronous dynamic passwords
    * Time based, synchronized with an authentication server
  * Asynchronous dynamic passwords
    * Does not use a clock
    * Based on an algorithm and an incrementing counter
* Biometrics
  * Type 3
  * Using a biometric factor instead of a username requires a one-to-many search
    * Capturing a single image of a person and searching a database of many people looking for a match
  * Using a biometric factor as an authentication technique requires a one-to-one match
    * The user claims an identity and the biometric factor is checked to see if the person matches the claimed identity
  * Retina scans
    * Pattern of blood vessels at the back of the eye
    * Most accurate
  * Iris scan
    * Second-most accurate
  * Palm scans
    * Measure vein patterns in the palm
  * Hand geometry
    * Physical dimensions of the hand
  * Signature dynamics
    * Writes a string of characters
  * Keystroke patterns
    * How the subject uses a keyboard
* Biometric Factor Error Ratings
  * False rejection rates
    * Type I error
  * False acceptance rates
    * Type II error
  * Crossover error rate (CER)
    * Where false rejection and false acceptance percentages are equal
    * Related to sensitivity of scan/detection
* Biometric registration
  * Enrollment
  * A subject's biometric factor is sampled and stored in a database
  * Known as a reference template/profile

#### Multifactor Authentication

* Must use multiple types/factors such as "something you know" and "something you have"
* Ex: Typing in a password (something you know), and then entering a synchronous dynamic password from a token (something you have)

#### Device Authentication

* Users can register their devices
* SecureAuth Identity provider (IdP)
* 802.1x

#### Implementing Identity Management

* Single sign on
  * Centralized access control
  * Allows a subject to be authenticated once on a system and to have access to multiple resources without authenticating again
* LDAP and centralized access control
  * Directory service
* LDAP and PKIs
  * LDAP and centralized access control systems can be used to support single sign on capabilities
* Kerberos
  * Key distribution center
    * KDC
    * Trusted third party that provides authentication services
  * Kerberos authentication server
    * Authentication service verifies or rejects the authenticity and timeliness of tickets
    * KDC
  * Ticket granting ticket
    * TGT
    * Provides proof that a subject has authenticated through a KDC and is authorized to request tickets to access other objects
  * Ticket
    * Encrypted message that provides proof that a subject is authorized to access an object
    * Sometimes called a Service Ticket (ST)
  * Know these processes
  * The Kerberos login process
    1. User types a username and password into a client
    1. The client encrypts the username with AES for transmission to the KDC
    1. The KDC verifies the username against a database of known credentials
    1. The KDC generates a symmetric key that will be used by the client and the Kerberos server, encrypts it with a hash of the user's password, and generates a time-stamped TGT
    1. The KDC transmits the encrypted symmetric key and the encrypted time-stamped TGT to the client
    1. The client installs the TGT for use until it expires and decrypts the symmetric key using a has of the user's password
  * The Kerberos ticket request steps
    1. The client sends its TGT back to the KDC with a request for access to the resource
    1. The KDC verifies that the TGT is valid and checks its access control matrix to verify that the user has sufficient privileges to access the requested resource
    1. The KDC generates a service ticket and sends it to the client
    1. The client sends the ticket to the server or service hosting the resource
    1. The server or service hosting the resource verifies the validity of the ticket with the KDC
    1. Once identity and authorization is verified, Kerberos activity is complete, and a session is opened

#### Federated Identity Management and SSO

* Single sign on
  * AKA SSO
* Security Assertion Markup Language
  * SAML
  * An XML-based language that is commonly used to exchange authentication and authorization (AA) information between federated organizations
* OAuth 2.0
  * Open standard used for access delegation
* Scripted access
  * Automated process to transmit logon credentials at the start of a logon session
* Credential management system
  * Storage space for suers to keep their credentials when SSO isn't available
* Integrating identity services
  * IDaaS
    * Identity as a service
    * A third party service that provides identity and access management
* AAA Protocols
  * Identification
  * Authentication
  * Authorization
  * Accountability
* RADIUS
  * Remote authentication dial in service
  * Centralizes authentication for remote connections
* TACACS+
  * Terminal access control access control system
  * An alternative to RADIUS
  * `+` includes moving AAA services into separate processes, encrypting authentication information
  * RADIUS only encrypts password
* Diameter
  * An enhanced version of RADIUS

#### Managing the Identity and Access Provisioning Lifecycle

* Refers to the creation, management, and deletion of accounts
* Provisioning
  * Creation of new accounts and provisioning them with appropriate privileges
  * Initial creation is called enrollment or registration
  * Should include a background check
  * Many organizations use automated provisioning systems
* Account review
  * Periodically ensure that security policies are being enforced
  * Check for inactive accounts
  * Excessive privilege
    * When users have more privileges than their assigned work tasks dictate
  * Creeping privileges
    * A user account accumulating privileges over time as job roles and assigned tasks change
  * Excessive and creeping privileges violate the principle of least privilege
* Account revocation
  * Disable user accounts as soon as possible when employees leave the organization
  * HR personnel should have the ability to perform this task
