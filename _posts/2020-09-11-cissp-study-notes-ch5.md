---
layout: post
title: CISSP Study Notes Chapter 5 - Protecting Security of Assets
date: 2020-09-11 07:30
author: thmsrynr
comments: true
categories: [cissp, security, certifications]
---
Chapter 5 is concerned with asset security. It discusses identifying and classifying information and assets, as well as determining how to maintain assets and identify asset owners. Chapter 5 also talks about protecting privacy, ensuring proper asset retention, determining data security controls, and establishing information and asset handling requirements.

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

## Chapter 5: Protecting Security of Assets

### My key takeaways and crucial points

#### Defining Sensitive Data

* *Sensitive data* is any data that isn't public or unclassified.
* *Personally identifying information* - PII. Can be used to identify an individual.
  * See NIST 800-122
  * Can distinguish or trace an individual's identity - ex: name, social security number, date and place of birth
  * Linked or linkable to an individual - ex: medical, financial, employment info
* *Protected health information* - PHI. Any health-related info that can be related to a specific person
  * HIPAA
  * Created or received by a healthcare provider
  * Relates to past, present or future physical or mental health or condition of an individual
  * HIPAA defines PHI more broadly
* Proprietary Data
  * Helps an organization maintain a competitive edge

#### Defining Data Classification

* *Data classification* - Identifying the value of the data to the organization.
  * Critical to protect data confidentiality and integrity
  * Classification labels
  * Identifies how data owners can determine proper classification
* Government uses top secret, secret, confidential, and unclassified
  * Top secret = "exceptionally grave damage"
  * Secret = "serious damage"
  * Confidential = "damage"
* Classifications also apply to physical/hardware assets
* Non-government
  * Use more meaningful labels - ex: confidential, proprietary, private, sensitive, public
  * More discretion
* Both systems identify relative value of data
  * Top secret is highest for governments
  * Confidential is highest for organizations

#### Data Classifications

* *Confidential or proprietary* - highest level of classified data
* *Private* - Should stay private within organization
* *Sensitive* - Similar to confidential, breach would cause damage to the mission of the organization
* *Public* - Unclassified data
* For the exam, remember *sensitive information* refers to anything that isn't public/unclassified

#### Defining Asset Classifications

* If a computer is processing top secret data, the computer is a top secret asset
  * Same with media
* Asset classification should match the data classifications

#### Determining Data Security Controls

* *Identity and Access Management* - IAM. See Chapter 13 and 14, but has to do with ensuring only authorized personnel can access resources.

#### Understanding Data States

* *Data at rest* - Stored on media.
* *Data in transit* - Data that is being transmitted over a network.
* *Data in use* - Data in memory or temporary storage while an application is using it.
* Protect confidentiality with strong encryption in all states

#### Marking Sensitive Data and Assets

* Most important information that a mark or label provides is the classification of data
* When users know the value of the data, they're more likely to protect it properly based on the classification
* Headers, footers, watermarks - DLP (data loss prevention) systems can identify documents that include sensitive information, apply appropriate controls
* Use labels for unclassified media to prevent errors of omission where sensitive data isn't marked
* If media or systems need to be downgraded to a less sensitive classification, it needs to be *sanitized*

#### Handling Sensitive Information and Assets

* Backup tapes should be protected with the same level of protection as the data that is backed up

#### Storing Sensitive Data

* Must store sensitive data such that it is protected against any type of loss
* Most obvious protection is encryption
* Do not neglect physical security practices
  * Theft, device failure
* The value of any sensitive data is much greater than the value of the media holding the sensitive data
  * It's more cost effective to purchase high quality backup media than to lose sensitive data

#### Destroying Sensitive Data

* NIST 800-88r1
* *Sanitization* - clearing, purging, and destroying to ensure data cannot be recovered by any means
  * When a computer is disposed of, sanitization means all nonvolatile memory is removed/destroyed

#### Eliminating Data Remanence

* *Data remanence* - Data that remains on media after the data was supposedly erased.
* *Degausser* - Generates heavy magnetic field to destroy data.
  * Cannot degauss SSDs (solid state drives)
  * Best method of sanitizing SSDs is destruction
* *Erasing* - Performing a delete operation against a file.
  * Only removes the directory or catalog link to data.
  * The data remains on the drive.
* *Clearing* - AKA overwriting.
  * Prepares media for re-use.
  * Unclassified data is written over all addressable locations on the media.
  * Maybe writing a single character or bit pattern over all media.
  * It is still possible to retrieve some of the original data using lab or forensics.
* *Purging* - More intense form of clearing.
  * Prepares media for reuse in less secure environments.
  * **The only method for reuse in less secure environments.**
  * Repeats the clearing process multiple times and may combine with other methods like degaussing to completely remove data.
* *Destruction* - Most secure method of sanitization.
  * Data cannot be extracted from destroyed media.
* *Declassification* - Any process that purges media or a system to prepare it for use in an unclassified environment.
  * Sanitization methods are often more effort than the cost for new media.

#### Ensuring Appropriate Asset Retention

* Record retention and media retention is the most important part of asset retention.
* *Record retention* - Maintaining important information as long as it is needed, destroying when it isn't.
* Companies cannot legal delete potential evidence after a lawsuit is filed.

#### Protecting Data with Symmetric Encryption

* Symmetric encryption uses the same key to encrypt and decrypt data
* *Advanced encryption standard* - AES.
  * Supports key sizes of 128 bits, 192 bits, and 256 bits.
* *Triple DES* - First implementation uses 56 bit keys.
  * New implementation uses 112 bit, 168 bit keys.
  * Longer keys is more secure.
* *Blowfish* - Key sizes between 32 bits and 445 bits.
  * Bcrypt adds 128 additional bits as a salt to protect against rainbow table attacks.

#### Protecting Data with Transport Encryption

* HTTP (Hypertext Transfer Protocol) operates in cleartext
* HTTPS (Hypertext Transfer Protocol Secure) adds encryption
  * Transport Layer Security (TLS) is current standard
  * Secure Sockets Layer (SSL) was precursor
* Virtual Private Networks (VPNs) create a logical tunnel between private networks
  * Allow employees in remote areas to access organizations internal network
  * Internet Protocol Security (IPSec) - VPN encryption
  * Layer 2 Tunneling Protocol (L2TP) - adds authentication header which provides authentication and integrity, and encapsulating security payload for confidentiality
  * IPSec and Secure Shell (SSH) is also commonly used

#### Data Owners

* *Data owner* - The person who has ultimate organizational responsibility for data
  * Establishes rules for appropriate use and protection
  * Input regarding security requirements and controls
  * Decides who has access to information and with what privileges
  * Assists in the identification and assessment of security controls
* NIST 800-18
  * Uses phrase "rules of behavior" which means Acceptable Use Policy

#### Asset Owners

* Also uses NIST 800-18
* *Asset owner* - Person who owns the asset or system that processes sensitive data
  * Develops a system security plan
  * Ensures system is deployed and operated according to security requirements
  * Delivers appropriate security training
  * Usually the same person as the data owner

#### Business/Mission Owners

* NIST 800-18 again
* *Business/Mission owner* - Program manager or information system owner
  * Might own processes that use systems managed by other entities

#### Data Processors

* *Data processor* - Any system used to process data
* GDPR defines as a "natural or legal person, public authority, agency, or other body, which processes personal data solely on behalf of the data controller.
  * Data controller controls the processing of data
* EU-US Privacy Shield
* Swiss-US Privacy Shield
* Privacy Shields are deep, but include
  * *Notice* - Organization must inform individuals about the purpose of data it collects
  * *Choice* - Offer a chance to opt out of data collection
  * *Accountability for onward transfer* - Can only transfer data to other organizations that comply with notice and choice principles
  * *Security* - Take reasonable precautions to protect personal data
  * *Data integrity and purpose limits* - Should only collect data that is needed for purposes in the notice
  * *Access* - Individuals must have access to information an organization holds about them, and to correct, amend or delete it
  * *Recourse, enforcement and liability* - Must implement mechanisms to ensure compliance and handle complaints
  * These are also general GDPR principles

#### Pseudonymization

* *Pseudonym* - An alias.
* *Pseudonymization* - Replacing data with artificial identifiers.
* *Tokenization* - Replacing data with tokens.
* Both methods can be reversed.

#### Anonymization

* *Anonymization* - The process of removing all relevant data so that it is impossible to identify the original subject or person.

#### More Terms

* *Data administrator* - Responsible for granting appropriate access to personnel.
* *Data custodian* - Data owners delegate day-to-day tasks to a custodian.
* *User* - Any person who accesses data to accomplish work tasks.

#### Protecting Privacy

* HIPAA (USA)
* Personal Information Protection and Electronic Documents (Canada)
* GDPR (EU)
* *Collection limitation principle* - The collection of data should be limited to only what is needed.

#### Using Security Baselines

* Baselines provide a starting point and ensure minimum security standards
* NIST 800-53 - Security Control Baselines are discussed
* *Scoping* - Reviewing a list of baseline security controls and selecting the ones that apply to the interesting IT system (the one you're trying to protect)
* *Tailoring* - Modifying the list of security controls within a baseline so they align with the mission of the organization
* PCI DSS (Payment Card Industry Data Security Standard)
  * For when business process major credit cards
* GDPR
  * Related to EU countries
