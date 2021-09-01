---
layout: post
title: CISSP Study Notes Chapter 20 - Software Devlopment Security
date: 2021-09-01 07:30
author: thmsrynr
comments: true
categories: [cissp, security, certifications]
---
Chapter 20 talks about understanding the security in the software development lifecycle, identifying and applying security controls in development environments, assessing the effectiveness of software security, assessing security impact of acquired software, and applying secure coding guidelines and standards.

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

## Chapter 20 - Software Devlopment Security

### My key takeaways and crucial points

#### Software Development

* Programming languages
  * Binary code - what computers understand, a series of 1s and 0s called machine language.
  * High level languages like Python, C++, Ruby, R, Java, Visual Basic allow programmers to write instructions that are better approximates for human communication.
  * Compiled languages like C, Java, FORTRAN use a compiler to convert the higher level language into an executable that the computer understands.
  * Interpreted languages like Python, R, JavaScript are not compiled and run in their original versions.
  * Compiled code is generally less prone to third party manipulation, but it is easier to hide malicious code. Compiled code is neither more nor less secure than interpreted.
* Object oriented programming
  * Each object in the OOP model has methods that correspond to specific actions that can be taken on the object, and inherit methods from their parent class
  * Provides a black-box approach to abstraction
  * Message - a communication to or input of an object
  * Method - internal code that defines the actions an object performs
  * Behavior - result of an object processing a method
  * Class - collection of common methods from a set of objects that defines behavior
  * Instance - objects are instances of a class
  * Inheritance - methods from a class are passed from a parent class to a child class
  * Delegation - forwarding a request by an objec tto another object
  * Polymorphism - the characteristic of an object that allows it to respond to different behaviors to the same message or method because of external condition changes
  * Cohesion - strength of the relationship between purposes of methods within the same class
  * Coupling - level of interaction between objects
* Assurance - properly implementing security policy through lifecycle of the System (according to the Common Criteria in a government setting)
* Avoiding and mitigating system failure
  * Input validation - when a user provides a value to be used in a program, make sure it falls within the expected parameters otherwise processing is stopped. Limit checks are when you check that a value falls within an acceptable range. Should always occur on the server side of a transaction.
  * Authentication and session management - require that users authenticate, and developers should seek to integrate apps with organizations existing authentication systems. Session tokens should exire, and cookies should only be transmitted over secure, encrypted channels.
  * Error handling - Errors should not expose sensitive internal information to attackers.
  * Logging - OWASP suggests logging these events: input validation failures, authentication attempts and failures, access control failures, tampering attempts, use of invalid or expired session tokens, exceptions raised by the OS or applications, administrative privilege usage, TLS failures, and cryptographic errors.
* Fail secure - high level of security
* Fail open - allows users to bypass failed security controls
* Software should revert to a fail-secure. This is what a Windows Blue Screen of Death does.
* Must balance security, functionality, user-friendliness.

#### Systems Development Lifecycle

* Conceptual definition - creating the basic concept statement for a system. Not longer than one or two paragraphs, and is agreed on by all interested stakeholders.
* Functional requirements determination - specific functionalities listed, devs start to think about how the parts of the system should interoperate. Think about input, behavior, output. Stakeholders must agree to this, too, and this document should be often referred to.
* Control specifications development - continues above design and review phases. Consider access controls, how to maintain confidentiality, provide an audit trail and a detective mechanism for illegitimate activity.
* Design review
* Code review walk-through - developers start writing code, walk through it looking for problems.
* User acceptance testing - actual users validate the system
* Maintenance and change management - ensure continued operation while requirements and systems change

#### Lifecycle Models

* Waterfall - Invented by Winston Royce in 1970. 7 stages, and each stage must be completed before the project moves to the next phase. Modern waterfall allows for moving backwards via "feedback loop". The first comprehensive attempts to model the software development process.
* Spiral - 1988 by Barry Boehm, allows for multiple iterations of a waterfall style process. System developers apply the whole waterfall process to the development of several prototypes, and return to the planning stages as demands and requirements change.
* Agile - emphasis on needs of the customer, quickly developing new functionality. Highest priority is to satisfy the customer through early and continuous delivery, handle changing requirements, prefer short timescales, collaboration.
* Gantt charts show interrelationships over time between projects and schedules. PERT is a project scheduling tool that relates estimated lowest possible size, most likely size, and highest possible size for each component.
* Change and configuration management - changes should be centrally logged.
  * Request control - users can request modifications, managers cna conduct cost/benefit analysis, and tasks can be prioritized
  * Change control - developers try to recreate situation encountered by the user, implements an organized framework, and allows devs to test a solution before rolling it out
  * Release control - changes are reviewed and approved, includes acceptance testing
  * Configuration identification
  * Configuration control
  * Configuration status accounting
  * Configuration audit
* DevOps - seeks to unify software development, quality assurance, and technology operations, rather than allowing them to operate in separate silos. Aims to decrease time required to develop and deploy software changes - you might even deploy several times a day.
* Application programming interfaces - APIs, allow websites to interact with each other by bypassing traditional webpages and interacting with the underlying service. May have authentication requirements.
* Software testing
  * Reasonableness check - Ensures the values returned by software match criteria, should be done via separation of duties
  * White box testing - step trhough code line by line
  * Black box testing - from a user's perspective
  * Gray box testing - combine white and black
  * Static testing - without running the code
  * Dynamic testing - done in a runtime environment
* Code repositories are a central storage point for developers to collaborate on source code.

#### Establishing Databases and Data Warehousing

* Hierarchical data model - logical tree structure, a one to many model
* Distributed data model - data stored in several databases that are logically connected
* Relational database - each table looks like a spreadsheet with row/column structure and a one to one mapping relationship
  * Candidate keys - subset of attributes that can uniquely identify a record in the table
  * Primary keys - selected from candidate keys to identify data. Only one primary key per table.
  * Foreign keys - used to enforce relationships between two tables (referrential integrity), and ensure that if one table contains a foreign key, it corresponds to a primary key in another table
* Database transactions - discrete sets of SQL instructions that will either succeed or fail as a group.
  * Must be committed to the database and cannot be undone when it succeeds.
  * ACID model
    * Atomicity - all or nothing
    * Consistency - consistent with all the database's rules
    * Isolation - transactions operate separately
    * Durability - once committed, they are preserved
* Security for multilevel databases
  * These contain information with a variety of different classifications, and must verify labels assigned to owners and provide only the appropriate information
  * Concurrency - edit control is a preventitive control that states information stored in the database is always correct. Locks allow one user to make changes but deny other users access at the same time.
  * Lost updates - when different processes make updates and are unaware of each other
  * Dirty reads - reading a record from a transaction that did not successfully commit
* Open database connectivity - a proxy between applications and backend database drivers that give programmers greater freedom in creating solutions without having to worry about the underlying database
* NoSQL - key/value stores that are good for high-speed applications, graph databases, and document stores.

#### Storing Data and Information

* Storage types
  * Primary/real memory - resources directly available to the CPU like RAM
  * Secondary storage - inexpensive, nonvolatile storage like hard drives
  * Virtual memory - simulate more primary memory via secondary storage
  * Random access storage - request conteints from any point within the media (RAM and hard drives)
  * Sequential access storage - needs to scan through the entire media, like a tape
  * Volatile storage - loses contents when power is removed (RAM)
  * Nonvolatile storage - does not depend on the presense of power
* Covert storage channels allow transmission of sensitive data between classification levels through the direct or indirect manipulation of shared storage media.

#### Understanding Knowledge Based Systems

* Expert systems - embody accumulated knowledge of experts. Have a knowledge base and an inference engine. Knowledge is codified  in a series of "if/then" statements.
* Inference engines examine information int he knowledge base to arrive at a decision.
* Machine learning
  * Supervised learning uses labeled data
  * Unsupervised learning uses unlabeled data
* Neural networks
  * Chains of computational units used to attempt to imitate biolgical reasoning processes of the human mind
  * Extension of machine learning
  * Aka deep learning
  * Delta rule - the ability to learn from experience
