---
layout: post
title: CISSP Study Notes Chapter 4 - Laws, Regulations, and Compliance
date: 2020-09-09 07:30
author: thmsrynr
comments: true
categories: [cissp, security, certifications]
---
Chapter 4 covers a variety of topics related to determining compliance requirements, contractual and legal standards, and privacy requirements. It also includes information to help you understand legal and regulatory issues that relate to information security in a global context like data breaches, licensing requirements, and privacy.

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

## Chapter 4: Laws, Regulations, and Compliance

### My key takeaways and crucial points

#### Categories of Laws

* *Criminal law* - Police and other law enforcement agencies are concerned with
  * Penalties include community service, fines, deprivation of civil liberties (prison time)
* *Civil law* - Contract disputes, employment matters, things that need impartial arbitration
  * Law enforcement doesn't normally become involved
  * Criminal prosecution, the government brings action against a person accused of a crime
* *Administrative Law* - Government charges agencies with purpose/function
  * Agencies abide by and enforce criminal and civil laws enacted by legislative branch
  * Published in the Code of Federal Regulations (CFR)

#### Laws

* General Data Protection Regulation (GDPR) - European Union
* Computer Fraud and Abuse Act (CFAA)
  * Based off of Comprehensive Crime Control Act of 1984 (CCCA)
  * Makes it a crime to (without authorization):
    * Access classified info or financial info in a federal system
    * Access a computer exclusively used by the federal government
    * Use a federal computer to perpetrate fraud
    * Cause malicious damage to a federal computer system in excess of $1000
    * Modify medical records on a computer when it may impair medical care
    * Traffic in computer passwords if it affects interstate commerce or involves a federal computer system
  * Federal computers was later extended to cover all "federal interest"
    * Computers used by US government
    * Computers used by financial institutions
* CFAA Amendments
  * Also covers interstate commerce in addition to federal interest
* Federal sentencing guidelines
  * Released in 1991
  * *Prudent man rule* - Senior executives must take personal responsibility for ensuring due care such that ordinary, prudent individuals would exercise in the same situation
  * *Burdens of proof for negligence*
    * Must have neglected a legally recognized obligation
    * Failure to comply with recognized standards
    * A relationship between the act of negligence and subsequent damages
* National Information Infrastructure Protection Act of 1996
  * Broadens CFAA to systems used in international commerce
  * Extends to include national infrastructure
  * Treats intentional and reckless acts that cause damage as a felony
* Federal Information Security Act - FISMA
  * Pertains to federal agencies
  * Includes activities of contractors
  * National Institute of Standards and Technology (NIST)
    * Responsible for developing FISMA implementation guidelines
    * Periodic assessments of risk
    * Policies and procedures
    * Plans for providing information security for networks, facilities, systems
    * Security awareness training
    * Testing and evaluation
    * Planning, implementing, evaluating, and documenting remedial actions
    * Detecting, reporting, and responding to security incidents
    * Ensure continuity of operations
* Federal Cybersecurity Laws of 2014
  * Centralizes federal cyber security responsibility to Homeland Security
  * Two exceptions
    * Defense related cyber security stays with Sec of Defense
    * Intelligence related issues stay with Director of National Intelligence
  * NIST charged with responsibility for coordinating nationwide work on voluntary standards
  * NIST SP 800-53 - Required for use in federal computing systems
  * NIST SP 800-171 - Often a contractual obligation for federal contractors

#### Intellectual Property (IP)

* Intangible assets are collectively referred to as intellectual property
* Copyright and the Digital Millennium Copyright Act
  * *Copyright law* - Guarantees the creators of original works of authorship are protected from unauthorized duplication of their work
  * Works covered:
    * Literary
    * Musical
    * Dramatic
    * Pantomimes and choreographic
    * Pictorial, graphical, and sculptural
    * Motion pictures and other audiovisual
    * Sound recordings
    * Architectural
  * Computer software is covered under the scope of literary work - the actual source code
  * Registering a copyright is not needed for copyright enforcement
    * Creators of work have an automatic copyright
  * Work for hire - when an employer pays for work in the normal course of a work day, the employer owns the copyright
  * Copyrights last until 70 years after the death of the last surviving author
  * Anonymous works are protected for 95 years from first publication or 120 years from date of creation - whichever is shorter
  * DMCA prohibits attempts to circumvent copyright protection
    * Also limits service provider liability
    * Not accountable for "transitory activities"
      * Transmission must be initiated by someone who is not a provider
    * Exempts activities of service providers related to system caching, but providers must take prompt action to remove copyright materials upon notification of infringement
    * One may make backup copies
* Trademarks
  * Words, slogans, logos, etc. used to identify a company and its products
  * Meant to avoid confusion in the marketplace
  * Automatically protected and can use the ™ symbol for public activities
  * For official recognition, apply to US Patent and Trademark Office
    * Registration certificate allows you to use the ® symbol
  * Must not be confusingly similar to another trademark
  * Should not be descriptive of the goods and services you'll offer
    * "Thomas' Software Company" is not a good trademark and may be rejected because it describes services
  * Trademarks are granted for 10 years and can be renewed for unlimited 10 year periods
* Patents
  * Protect IP rights of inventors for 20 years
  * Inventions must...
    * Be new
    * Be useful
    * Not be obvious - ex: using a drinking cup to collect rainwater is obvious, but a specially designed cup that limits evaporation might not be
  * *Patent trolls* register patents, manipulate the system and rules to sue or otherwise make monetary gain from patents, often without creating the invention actually patented
* Trade Secrets
  * IP that is critical to a business
  * Significant damage would result if disclosed competitors or public
  * Filing copyright or patent requires you publicly disclose the details, no longer secret
    * Are also time-limited
  * Trade secrets are things you want to keep to yourself
  * Enforced by nondisclosure agreements (NDA)
  * Patent law does not provide adequate protection for software products, so it's often treated as a trade secret
* Licensing
  * *Contractual license* - written contract
  * *Shrink-wrap license* - a clause stating you acknowledge agreement simply by "breaking the seal on the shrink wrap"
  * *Click-through license* - increasingly common, required to click a button, adds active consent
  * *Cloud services license* - click-through agreements to the extreme

#### Import/Export

* International Traffic in Arms Regulations (ITAR) - controls export of items designated as military and defense items
* Export Administration Regulations (EAR) - covers items designed for commercial use by t may have military applications
* Computer Export Controls
  * US firms can export computers almost anywhere without permission, with exceptions
  * Exceptions from Department of Commerce's Bureau of Industry and Security
  * Exceptions based on nuclear threat
  * Exceptions that need permission are currently Cuba, Iran, North Korea, Sudan, and Syria

#### Privacy

* US Privacy Law
  * No constitutional guarantee of privacy - many federal laws exist
  * Fourth Amendment - prohibits government agents from searching private property without a warrant and probably cause
    * Also includes protection against wiretapping and other privacy invasions
  * Privacy Act of 1974
    * Severely limits federal government ability to disclose private information to other people or agencies without written consent of affected individuals
    * Only applies to government agencies
  * Electronic Communication Privacy Act of 1986
    * Make sit a crime to invade the electronic privacy of an individual
* Communications Assistance for Law Enforcement Act (CALEA) of 1994
  * Requires communications carriers to make wiretaps possible
* Health Insurance Portability and Accountability Act of 1996 (HIPAA)
  * Governs health insurance and health maintenance organizations
  * Hospitals, physicians, insurance companies
  * Defines the rights of individuals
* Health Insurance Technology for Economic and Clinical Health Act of 2009 (HITECH)
  * Change in the ways laws treats business associates
  * New data breach notification requirements
  * Must notify Health and Human Services and the media when a breach impacts more than 500 individuals
* Children's Online Privacy Protection Act of 1998 (COPPA)
  * Websites must have a privacy notes
  * Parents need an opportunity to review any information collected from their children
  * Parents must give verifiable consent to collection of information of children under the age of 13 before it's collected
* Gramm-Leach-Bliley Act of 1999 (GLBA)
  * Banks, insurance companies, credit providers
  * Information the above can share with each other
* USA PATRIOT Act of 2001
  * The way government can obtain wiretapping authorization
  * ISPs may provide government with a large range of information
* Family Educational Rights and Privacy Act (FERPA)
  * Educational institutions that accept any form of funding from federal government
* Privacy in the workplace
  * There is a reasonable expectation of privacy when you mail a letter, etc.
  * Employees do not have a reasonable expectation of privacy while using employer-owned communications equipment in the workplace
  * Consider:
    * Clauses in employment contracts
    * Acceptable use and privacy policies
    * Logon banners
    * Warning labels
* European Union General Data Protection Regulation (GDPR)
  * May 28, 2018
  * Widened scope of regulation
  * Applies to all organizations that collect data from EU residents or process it on behalf of someone else
  * Applies to organizations that are not based in the EU
  * Key provisions
    * Breach notifications must occur within 24 hours
    * Individuals will have access to their own data
    * Right to be forgotten - able to delete data

#### Compliance

* Payment Card Industry Data Security Standard (PCI DSS)
