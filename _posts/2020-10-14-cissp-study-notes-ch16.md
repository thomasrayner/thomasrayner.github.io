---
layout: post
title: CISSP Study Notes Chapter 16 - Managing Security Operations
date: 2020-10-14 07:30
author: thmsrynr
comments: true
categories: [cissp, security, certifications]
---
Chapter 16 goes over securely provisioning resources, understanding and applying foundational security operations concepts, applying resource protection techniques, implementing and supporting patch and vulnerability management, understanding and participating in change management, and addressing personnel safety and security concerns.

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

## Chapter 16: Managing Security Operations

### My key takeaways and crucial points

#### Applying Security Operations Concepts

* Due care and due diligence refers to taking reasonable care to protect the assets of an organization on an ongoing basis
* Need to know
  * Focuses on permissions and the ability to access information
  * Rights
    * Refers to the ability to take actions
  * Grant users access only to data or resources they need to perform assigned work tasks
* Least privilege
  * Granted only the privileges necessary to perform assigned work tasks and no more
  * Entitlement
    * The amount of privileges granted to users
  * Aggregation
    * The amount of privileges that users collect over time
  * Transitive trust
    * A trust relationship between two security domains
* Separation of privilege
  * No single person has total control
  * Collusion
    * An agreement by two or more persons to perform some unauthorized activities
  * Helps reduce fraud
  * Builds on least privilege
  * Segregation of duties is specifically required by SOX
* Two person control
  * Operations that require two keys
  * Ensures peer review, reduces likelihood of fraud
  * Split knowledge is where information or privilege is divided among multiple users
* Job rotation
  * Encourages peer review, reduces fraud, enables cross training
  * Acts as both a deterrent and a detection mechanism
* Mandatory vacations
  * Peer review, helps detect fraud and collusion
  * Acts as a deterrent and a detection mechanism

#### Privileged Account Management

* Special privilege operations
  * Activities that require special access or elevated rights and permissions to perform
  * Sensitive job tasks
* Monitoring usage of special privileges, so organizations can deter employees from misusing privileges and detect actions
* Perform access review audits

#### Managing the Information Lifecycle

* Creation/capture
  * Data is created by users, downloading files, etc.
* Classification
  * Should be done asap
  * Ensure that sensitive data is identified and handled appropriately based on its classification
  * Once data is classified, it can be marked and handled correctly
    * Easily recognize data's value
* Storage
  * Periodically back up
  * Encrypted
  * Physical security
* Usage
  * Any time data is in use or in transit over a network
  * Used in an unencrypted format
* Archive
  * Comply with laws/regulations regarding data retention
  * Ensure data is available
* Destruction/purging
  * NIST 800-88r1

#### Service Level Agreements

* Defines performance expectations and penalties
* Sometimes have memorandums of understanding
  * and/or an interconnection security agreement
  * Two entities work together toward a common goal
* Can specify technical requirements

#### Addressing Personnel Safety and Security

* Always possible to replace equipment and data, can't replace people
* Human safety is **ALWAYS** top priority
* Duress
  * A simple duress system is just a panic button that sends a distress call
  * More common when working alone
  * Code words or phrases
* Travel
  * Verify a person's identity before opening a hotel door
  * Sensitive data is ideally not brought on the road, but if it is it needs to be encrypted
  * Malware/monitoring devices
    * Maintain physical control of all devices
    * Do not bring personal devices
  * Free WiFi
    * Vulnerable to man in the middle attacks
* Emergency management
  * Natural or man-made disasters
  * Locate sensitive physical assets toward the center of the building

#### Managing Virtual Assets

* Reduction in overall operating costs when going virtual
* Hypervisor
  * Essential virtualization software

#### Managing Cloud Based Assets

* SaaS
  * Software as a service
  * Fully functional applications accessed via web browser, usually
* PaaS
  * Platform as a service
  * Computing platform, including hardware, an OS, and applications
* IaaS
  * Infrastructure as a service
  * Basic computing resources
* NIST 800-145
* Public cloud
  * Available for any consumers
* Private cloud
  * Single organization
* Community cloud
  * Two or more organizations
* Hybrid cloud
  * Combination of two or more clouds

#### Media Management

* Includes any hard copy of data
* When media is marked, handled and stored properly, it helps prevent unauthorized disclosure (loss of confidentiality), unauthorized modifications (loss of integrity), and unauthorized destruction (loss of availability)
* Tape media
  * Keep at least two copies of backups
  * At least one offsite
* Mobile devices
  * MDM system monitors and manages devices, ensures they are up to date
  * Encryption protects data if phone is lost or stolen
* Managing media lifecycle
  * Once backup media has reached it's MTTF, it should be destroyed
  * Degaussing does not remove data from an SSD

#### Managing Configuration

* Baselining
  * Baselines are starting points
  * When systems are deployed in a secure state with a secure baseline, they are more likely to stay secure
* Using images for baselining
  1. Create the image
  2. Capture the image
  3. Deploy the image
* Ensure that desired security settings are always configured correctly

#### Managing Change

* Change management
  * Reducing unanticipated outages by unauthorized changes
  * Primary goal is to ensure that changes do not cause outages
* Unauthorized changes directly affect availability
* Security impact analysis
  1. Request the change, identify desired changes
  2. Review the change
  3. Approve/reject the change
  4. Test the change
  5. Schedule and implement the change when it will have the least impact
  6. Document the change
* Emergency changes can still occur, but the process still needs to document the changes
* Versioning
  * Labeling or numbering system that differentiates between different software sets and configurations across multiple machines or at different points in time on a single machine
* Configuration documents
  * Who is responsible
  * Purpose of the change
  * List all changes to the baseline

#### Managing Patches and Reducing Vulnerabilities

* Systems to manage
  * Any computing device with an OS
  * Network infrastructure systems
  * Embedded systems
* Patch management
  * Patch
    * Any type of code written to correct a bug or vulnerability or improve the performance of existing software
  * Evaluate patches
    * Determine if they apply to your systems
  * Test patches
    * Test on an isolated nonproduction system
    * Determine unwanted side effects
  * Approve the patches
    * Change management
  * Deploy the patches
    * Automated methods
  * Verify that patches are deployed
    * Regularly test and audit systems
* Vulnerability management
  * Identifying vulnerabilities, evaluating them, mitigating risks
  * Vulnerability scans
    * Test systems and networks for known security issues
    * Nessus by Tenable Network Security
    * Generate reports
  * Vulnerability assessments
    * Scan reports from past year to determine if the organization is addressing vulnerabilities
    * "Why hasn't this been mitigated?"
    * Part of a risk analysis or assessment
  * Common vulnerabilities and exposures
    * MITRE maintains the CVE database: cve.mitre.org
    * MITRE is not an acronym, funded by US government to maintain the database
