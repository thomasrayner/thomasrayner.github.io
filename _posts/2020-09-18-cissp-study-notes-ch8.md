---
layout: post
title: CISSP Study Notes Chapter 8 - Principles of Security, Models, Design, and Capabilities
date: 2020-09-18 07:30
author: thmsrynr
comments: true
categories: [cissp, security, certifications]
---
Chapter 8 covers implementing and managing engineering processes using secure design principles, the fundamental concepts of security models, how to select controls based on security requirements, and understanding security capabilities of information systems.

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

## Chapter 8: Principles of Security, Models, Design, and Capabilities

### My key takeaways and crucial points

#### Objects and Subjects

* *Subject* - The user or process that makes a request to access a resource
* *Object* - The resource a subject wants to access
* *Transitive trust* - If A trusts B, and B trusts C, then A inherits trust of C through B
  * May enable bypassing of restrictions or limits between A and C

#### Closed and Open Systems

* *Closed system* - Designed to work well with a narrow range of other systems
* *Open system* - Designed using agreed-upon industry standards
* **This is different than closed/open source**
* Attacking a closed system is harder

#### Techniques for Ensuring CIA

* *Confinement* - Allows a process to read from and write to only certain memory locations and resources
* *Bounds* - Processes are assigned an authority level
  * Bounds of a process consist of limits set on the memory locations and resources it can access
* *Isolation* - Enforcing access bounds. Used to protect the operating environment, the kernel of the OS, and other applications
* *Controls* - Uses access rules to limit the access of a subject to an object
  * *MAC* - Mandatory access control
  * *DAC* - Discretionary access control
  * Chapter 14 is all about this topic
  * Each subject has attributes that define clearance/authority/access to resources
  * Each object has attributes that define it's classification
* *Trust and Assurance* - Security issues should not be added on as an afterthought
  * *Trusted system* - One where all protection mechanisms work together to process sensitive data for different users while maintaining a secure computing environment.
  * *Assurance* - The degree of confidence in the satisfaction of security needs
  * When change occurs, the system needs to be reevaluated

#### Understand the Fundamental Concepts of Security Models

* *Security model* - A way for designers to map abstract statements into a security policy
* *Token* - A separate object associated with a resource and describes its security attributes
* *Capabilities list* - Maintains a row of security attributes for each controlled object
* *Security label* - A permanent part of the object to which it's attached
* *Trusted computing base* - TCB. A combination of hardware, software, and controls that work together to form a trusted base to enforce your security policy
* *Security perimeter* - An imaginary boundary that separates Trusted Computing Base from the rest of the system
* *Trust paths* - Secure channels for Trusted Computing Base to talk to the rest of the system
* *Reference monitor* - Part of TCB that validates access to every resource. Stands between every subject and object, verifying requests
* *Security kernel* - Collection of components in TCB that work together to implement reference monitor functions
* *State machine model* - Describes a system that is always secure no matter what state it's in
* *State* - A snapshot of a system at a specific moment in time
* *Information flow model* - Focuses on the flow of information based on a state machine model
  * Discussed later in this chapter
  * *Bell-LaPadula* - Concerned with information flow from high security level to a low security level
  * *Biba* - Concerned with preventing information flow from a low security level to a high security level
* *Noninterference* - Concerned with how the actions of a subject at a higher security level affect the system state or the actions of a subject at a lower security level
  * Isolation
* *Take-Grant model* - Employs a directed graph to dictate how rights are passed from one subject to another, or from a subject to an object
* *Access Control Matrix* - A table of subjects and objects that indicates the actions or functions each subject can perform on each object
  * Each row has a *capabilities list* - Access Control List (ACL). Tied to the subject and lists valid actions that can be taken on each object
* Lattice-Based Access Control
  * *Simple property* - Concerned with reading data
  * *Star property* - Concerned with writing data

#### Bell-LaPadula Model

* US Department of Defense developed in 1970s
* Concerned with protecting classified information
* A subject with any level of clearance can access resources at or below its clearance level
* Prevents leaking or transfer of classified information to less secure clearance levels
* Does not address integrity or availability
* No read up (simple property)
* No write down (star property)
* Uses an access control matrix (discretionary property - need to know)

#### Biba Model

* Integrity is more important than confidentiality
* Also built on state machine concept, based on information flow, and is multilevel
* Very similar to Bell-LaPadula, except inverted
* No read down (simple property)
* No write up (star property)

#### Clark-Wilson Model

* Does not use lattice structure, but rather uses *access triple control*
  * Subject
  * Program/transaction
  * Object
* Objects are accessed only through programs
* *Constrained data item* - CDI. Any data item whose integrity is protected by the security model
* *Restricted interface model* - Elements of an interface are limited based on a subjects rights and authorization

#### Brewer and Nash Model (aka Chinese Wall)

* Changes dynamically based on a user's previous activity
* *Chinese Wall model* - Creates a class of data that defines which security domains are potentially in conflict and prevents subjects with access to one domain that belongs to a specific conflict class from access any other information in the conflict class
* Protects from conflicts of interest

#### Goguen-Meseguer Model

* Integrity model, less well known as Biba
* Foundation of noninterference conceptual theories

#### Sutherland Model

* Integrity model, focused on preventing interference

#### Graham-Denning Model

* Focused on the secure creation and deletion of both subjects and objects
* A collection of eight protection rules or actions that define boundaries (**Only one with all eight**)
  * Create an object
  * Create a subject
  * Delete an object
  * Delete a subject
  * Provide read access right
  * Provide grant access right
  * Provide delete access right
  * Provide transfer access right

#### Select Security Controls Based On Systems Security Requirements

* Need a tested and technical evaluation
* Need a formal comparison of its design and security criterial
* Sometimes you may need a trusted third party to provide a *seal of approval*
* *Trusted Computer System Evaluation Criteria* - TCSEC. Standards to attempt to specify minimum security criteria for various categories of use
  * Classes and required functionality
    * D - Minimal protection
    * C1 - Discretionary protection
    * C2 - Controlled access protection
    * B1 - Labeled security
    * B2 - Structured protection
    * B3 - Security domains
    * A1 - Verified protection
* *Common Criteria* - Represents a global effort that is similar to TCSEC in function/purpose
  * Assurance levels
  * EAL1 - Functionally tested
  * EAL2 - Structurally tested
  * EAL3 - Methodically tested and checked
  * EAL4 - Methodically designed, tested, and reviewed
  * EAL5 - Semi-formally designed and tested
  * EAL6 - Semi-formally verified, designed, and tested
  * EAL7 - Formally verified, designed, and tested
* Industry and International Security Implementation Guidelines
  * Payment Card Industry Data Security Standard (PCI DSS)
  * International Organization for Standardization (ISO)
* *Certification* - Comprehensive evaluation of security features of an IT system
* *Accreditation* - A formal declaration by the designated approval authority that an IT system is approved to operate in a particular security mode
  * Often an iterative process

#### Understand Security Capabilities of Information Systems

* *Virtualization* - Used to host one or more operating systems within the memory of a single host computer
* *Trusted Platform Module* - TPM. Specification for a cryptoprocessor chip on a mainboard, and the general name for implementation of the spec
  * Stores and processes cryptographic keys
* *Hardware security module* - HSM. A cryptoprocessor used to manage/store digital encryption keys, accelerate crypto operations, support faster digital signatures, improve authentication
* *Interfaces* - Implemented with an application to restrict what users can do or see based on their privileges
* *Fault tolerance* - The ability of a system to suffer a fault but continue to operate
