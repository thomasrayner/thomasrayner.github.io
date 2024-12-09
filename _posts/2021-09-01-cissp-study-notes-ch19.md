---
layout: post
title: CISSP Study Notes Chapter 19 - Investigations and Ethics
date: 2021-09-01 07:30
author: thmsrynr
comments: true
categories: [cissp, security, certifications]
---
Chapter 19 covers how to understand, adhere to, and promote professional ethics, understanding and supporting investigations, and understanding different investigation types.

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

## Chapter 19 - Investigations and Ethics

### My key takeaways and crucial points

#### Investigations

* *Administrative investigations* - internal investigations that examine either operational issues or a violation of the organization's policies. May transition to another type of investigation.
* *Root cause analysis* - determine the reason that something occured.
* *Criminal investigations* - conducted by law enforcmenet, related to alleged violation of criminal law. Must meet "beyond a reasonable doubt" standard which states there are no other logical conclusions.
* *Civil investigations* - do not involve law enforcement, but involves internal employees and outside consultants working for a legal team. Must meet the weaker "preponderance of the evidence" standard that demonstrates the outcome is more likely than not. Not as rigorous.
* *Regulatory investigations* - government agencies do these when they think there's been a violation of administrative law. Violations of industry standards.
* Electronic discovery
  * *Information governance* - info is well organized
  * *Identifification* - locates the information
  * *Preservation* - protected against alteration or deletion
  * *Collection* - gatehrs the responsive information centrally
  * *Processing* - screens the collected information
  * *Review* - determine what information is responsive to the event
  * *Analysis* - deeper inspection
  * *Production* - place info in a format that it may be shared
  * *Presentation* - show info to witnesses, the court, other parties
* *Admissible evidence* - must be relevant to determining a fact, material/related to the case, competent (obtained legally)
* Evidence types
  * *Real* - things that may actually be brought into a court of law, aka conclusive evidence
  * *Documentary* - written items brought to court to prove a fact at hand
  * *Testimonial* - testimony of a witness, can be direct evidence based on their observations, or expert opinions
  * *Hearsay* - something that was told to someone outside of court - not admissible
* *Best evidence rule* - original documents must be introduced, not copies
* *Parol evidence rule* - when an agreement between parties is put into writing, the document is assumed to contain all the terms of the agreement and that no verbal agreement may modify the written agreement
* Chain of evidence/custody
  * Evidence should be labled with general description, time and date of collection, location evidence was collected from, name of collector, relevant circumstances

#### Evidence Collection and Forensic Procedures

* Actions taken to collect should not change evidence
* Person should be trained to access evidence
* All activity related to evidence should be fully documented, preserved, available for review
* Individuals are responsible for all actions taken
* Preserve the original evidence
* *Network analysis* - when incidents take place over a network. Often difficult to reconstruct because networks are volatile, and depend on prior knowledge than an incident is underway or logs.
* *Software analysis* - reviews of applications or activity, or review of software code and log files.
* *Hardware/embedded device analysis* - includes memory, storage systems

#### Investigation Process

* *Rules of engagement* - define and guide investigative actions
* Gathering evidence
  * *Voluntary surrender* - given up willingly, usually when the attacker is not the owner
  * *Subpoena* - or court order, the court compels someone to provide evidence, but this gives the data owner time to alter the evidence and ruin it
  * *Search warrant* - used when you must have access to evidence without alerting evidence owner or other personell, the court allows you to seize evidence
* Deciding whether or not to involve law enforcement is challenging because incidents are more likely to become public, and the Fourth Amendment hampers government investigators in ways that private companies are not.
* Never conduct investigations on an acutal system that was compromised. Take them offline and use backups.
* Do not attempt to "hack back" and avenge a crime.
* Call in expert assistance if needed.
* Interviewing - gather information from an individual. If information is presented in court, the interview is an interrogation.
* Attackers often try to santize log files after attacking, so to preserve evidence, logs should be centralized remotely.
* A final report should be produced by any investigation that details the processes followed, evidence collected, and final results of investigation. Lays the foundation for escalation and legal action.

#### Major Categories of Computer Crime

* *Computer crime* - violation of law that invovles a computer. Any individual who violates your security policies is an attacker.
* *Military and intelligence attacks* - restricted ifnormation from law enforcement or military and research sources
* *Business attacks* - focus on illegally obtaining confidential information. Aka corporate espionage or industrial espionage. Stealing trade secrets.
* *Financial attacks* - carried out to unlawfully obtain money or services. Ex: shoplifting, burglary.
* *Terrorist attacks* - to disrupt normal life and instill fear, as opposed to military or intelligence attack which is designed to extract secret information.
* *Grudge attacks* - to do damage to an organization or person, usualy out of resentment or to "get back at" an organization. Insider threat is big, these attacks can come from disgruntled employees.
* *Thrill attacks* - done for "the fun of it", usually by "script kiddies". May also be related to "hacktivism".

#### Ethics

* Rules that govern personal conduct
* Codes of ethics are not laws, but standards for professional behavior

> You should study and review the ISC2 Code of Ethics prior to taking your CISSP exam
