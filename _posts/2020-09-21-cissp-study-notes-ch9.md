---
layout: post
title: CISSP Study Notes Chapter 9 - Security Vulnerabilities, Threats, and Countermeasures
date: 2020-09-21 07:30
author: thmsrynr
comments: true
categories: [cissp, security, certifications]
---
Chapter 9 gets into assessing and mitigating the vulnerabilities of security architectures, designs, and solution elements. It also talks about assessing and mitigating vulnerabilities in web-based systems, mobile systems, and embedded devices.

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

## Chapter 9: Security Vulnerabilities, Threats, and Countermeasures

### My key takeaways and crucial points

#### Processor

* *Computer architecture* - Engineering discipline related to design and construction of computer systems at a logical level
* *Processor* - Central Processing Unit (CPU). The chip that governs all major operations and either performs or coordinates calculations that allow a computer to perform its tasks
  * Execution types:
    * *Multitasking* - Handling two or more tasks simultaneously
    * *Multicore* - A single microprocessor chip that contains independent execution cores
    * *Multiprocessing* - A computing system with more than one CPU uses the power of more than one processor to complete a multithreaded operation
    * *Massively parallel processing* - MPP. Hundreds or more processors with their own OS and resources, coordinated by software to perform in unity
    * *Multiprogramming* - Similar to multitasking
    * *Multithreading* - Multiple concurrent tasks are performed within a single process - multitasking involves multiple processes
  * Processing types:
    * *Single state* - Use the policy mechanisms to manage information at different levels
    * *Multistate* - Implement higher levels of security by using mechanisms
      * *Protection rings* - Organize code and components in an OS into concentric rings.
        * Deep inside ring is 0, highest level of privilege and can access anything.
        * *Kernel* - Part of the OS that remains resident in memory so it can be run on demand at any time. Lives in ring 0.
        * Ring 1 houses the rest of the OS
        * Ring 2 is somewhat privileged, I/O drivers and other system utilities reside
        * Applications and programs live in Ring 3
      * *Process states* - Aka operating states
        * *Supervisor state* - privileged, all access
        * *Problem state* - Associated with user mode where privileges are low and access requests must be checked
        * *Ready* - Process is ready to resume or start processing as soon as it is scheduled
        * *Waiting* - Process is waiting for a resource, waiting for continued execution but a device or access request is to be serviced first
        * *Running* - Executing on the CPU and goes until it finishes or it's time slice expires or it is blocked
        * *Supervisory* - When the process must perform an action that requires privileges that are greater than the problem state's set of privileges
        * *Stopped* - When a process finishes or errors out, it becomes "stopped" so the OS can recover memory and other resources
* Security modes
  * See chapter 1 for data classification
  * *Dedicated mode* - Single state system where each user must have a security clearance that permits access to all information on the system, and *need to know* for all information
  * *System high mode* - Each user needs a valid security clearance that covers all information on the system, but only *need to know* for some information
  * *Compartmented mode* - Same as above, but they only need approval to access some information, not all
  * *Multilevel mode* - Same as above, except users don't need clearance for all information, just pursuant to it's classification
* Operating modes
  * *User mode* - The basic mode a CPU uses when executing user applications
  * *Privileged mode* - Gives the OS access to the full range of instructions supported by the CPU

#### Memory

* *Read-Only memory* - ROM. Memory the PC can read but cannot change
* *Programmable Read-Only memory* - PROM. Similar to a ROM chip but can be programmed separately from manufacturing, but only once
* *Erasable Programmable Read-Only memory* - EPROM. Ultraviolet EPROMs can be erased with a light
* *Electronically Erasable Programmable Read-Only memory* - EEPROM. Electronically erasable PROM
* *Flash memory* - Derivative from EEPROM, can be electronically erased and rewritten, can be erased in blocks or pages
* *Random Access Memory* - RAM. Readable and writable memory that contains information a computer uses during processing
  * *Real memory* - The largest RAM storage resource available, made of dynamic RAM chips
  * *Cache RAM* - Caches that improve performance by taking data from slower devices and storing it temporarily in faster devices when repeated use is likely
* *Registers* - Limited onboard memory in a CPU
* Memory addressing
  * *Register addressing* - An identifier for a register
  * *Intermediate addressing* - A way of referring to data that is supplied to the CPU as part of an instruction
  * *Direct addressing* - CPU is provided with an actual address of the memory location to access
  * *Indirect addressing* - Similar to direct, however the address supplied doesn't contain the actual value, it contains another memory address
  * *Base+Offset addressing* - Uses a value stored in one register as the base from which to begin counting, and then adds the offset supplied to retrieve a value from that computed memory location
* *Secondary memory* - Usually magnetic, optical, flash-based, or other storage that contains data not immediately available for the CPU - Hard drives, DVDs, etc.

#### Storage

* *Data storage devices* - Used to store information that may be used any time after it's written
* *Primary vs secondary* - Primary storage is RAM. Secondary is long-term storage like hard drives.
* *Volatile vs non-volatile* - Volatile devices lose their data when they lose power
* *Random vs sequential* - Random access storage allow an OS to read immediately from any point. Sequential storage doesn't.
* Storage media security
  * *Data remanence* - Data may remain on devices after it is erased
  * SSDs can only be sanitized by destroying them
  * Prone to theft, important to use full disk encryption

#### Input and Output Devices

* Monitors - Primary concern is *shoulder surfing* - looking over the shoulder or at the screen to observe information displayed
* Printers - Users may leave sensitive printouts, some printers store data locally and can re-print data
* Keyboards/mice - Key loggers may intercept and record key strokes and transmit them, revealing passwords and other sensitive information
* *Firmware* - Software stored on a ROM chip
  * *BIOS* - Basic input/output system. Contains OS independent primitive instructions that a computer needs to start up and load the OS from disk.
  * Device firmware also needs limited processing

#### Client-Based Systems

* *Client-side attack* - Any attack that is able to harm a client, may occur over any protocol
* *Applets* - Code objects that are sent from a server to a client to perform some action - mini programs
* *Local cache* - Anything that is temporarily stored on the client for future reuse - see ARP caches, the chapter goes into a ridiculous amount of detail on ARP attacks and DNS cache poisoning

#### Server-Based Systems

* *Data flow control* - The movement of data between process, between devices, across a network, or over communication channels
  * Making sure endpoints are not overwhelmed with traffic - maybe by using a *load balancer*
* *Denial of service attack* - Attacking the availability of a resource or system, often by attacking data flow control

#### Database Systems Security

* *Aggregation* - Combining records from one or more tables to produce potentially useful information
  * An attacker might be able to take multiple pieces of seemingly innocuous information, and combine them to infer something more dangerous
* *Inference* - Combining several pieces of non-sensitive information to gain access to information that should be classified at a higher level
* *Data mining* & *data warehousing* - Warehouses are large databases, data dictionaries are used for storing critical information about data, mining allows analysts to comb through warehouses and look for correlated information
* *Data analytics* - The science of raw data examination with the focus of extracting useful information out of the bulk information set
  * *Big data* - Collections of data that have become so large that traditional means of processing aren't enough
* *Large-Scale parallel data systems* - Systems designed to perform numerous calculations simultaneously

#### Distributed Systems and Endpoint Security

* *Distributed architecture* - The concept of a client-server model network
  * Email needs to be screened
  * Download/upload policies must be created
  * Systems must be subject to robust access controls
  * Restrict user-interface mechanisms and database management systems
  * File encryption may be appropriate, but full disk encryption is also needed
  * Separate and isolate processes that run in user and supervisory mode
  * Protection domains should be created
  * Sensitive materials must be labeled
  * Files on user machines should be backed up
  * Users need regular security awareness training
  * Computers and their storage media require protection from environmental hazards
  * User computers should be included in disaster recovery and business continuity planning
  * Developers of custom software need to take security into account
* *Cloud computing* - Referring to computing where processing and storage are performed elsewhere over a network connection rather than locally - Depends on virtualization
  * *Type 1 hypervisor* - Native or bare-metal hypervisor, there is no host OS, the hypervisor installs directly on the hardware
  * *Type 2 hypervisor* - Hypervisor software is installed on top of another OS
  * *Cloud storage* - Using storage provided by a cloud vendor to host data for an organization
  * *Elasticity* - The flexibility to expand or contract based on need
  * *Platform as a service* - PaaS. Providing a computing platform and software stack as a virtual service
  * *Software as a service* - SaaS. Providing on-demand online access to software applications without need for local installation
  * *Infrastructure as a service* - IaaS. Providing on-demand outsourcing options for operating solutions
  * *Hosted solution* - A deployment concept where the organization must license software and then operates and maintains the software - the hosting provider takes care of the hardware that supports the organization's software
  * *Private cloud* - Service within a corporate network and isolated from the internet, internal use only
  * *Public cloud* - Services are accessible to the general public over an internet connection, usually paid for with subscriptions or pay-per-use, could be free. Data is separated and isolated from other customers, but the overall purpose of the cloud is the same for all customers
  * *Hybrid cloud* - A mix of public and private
  * *Community* - A shared environment used and paid for by a group of users or organizations for shared benefit
* *Grid computing* - Parallel distributed processing that groups processing nodes to work towards a specific goal
* *Peer to peer* - Share tasks and workloads among peers, like grid computing, but there is no central management system

#### Internet of Things

* *Smart devices* - Mobile devices that have customization options, apps, on-device or in-cloud AI
* *Internet of things* - IoT. A class of smart devices that are internet-connected to provide automation, remote control, or AI processing to traditional or new devices
* Often not designed with security in mind

#### Industrial Control Systems

* *Industrial control system* - ICS. Computer management device that controls industrial processes an machines
* *SCADA* - Supervisory control and data acquisition. Can operate as a stand-alone device, or networked together with other systems.

#### Assess and Mitigate Vulnerabilities in Web-Based Systems

* *Open web application security project* - OWASP. A nonprofit security project focused on improving security for online applications. Also a large community.
  * See their Top 10 critical attacks for an idea of what's hot right now
* *Injection attack* - Exploitation where an attacker can submit code to a system to modify its operations
  * SQL injection are related to SQL queries and databases
* *Input validation* - Limiting the types of data a user provides in a form. Input sanitization can happen here and should include escaping metacharacters.
  * *Escaping metacharacters* - The process of marking the metacharacter as merely a normal or common character, such as a letter or number, thus removing it's special programmatic powers
* Limit account privileges - the database account that the web server uses should only have the rights to do the limited operations it's expected to perform
* *Directory traversal* - An attack that enables an attacker to jump out of the web root directory structure and into other parts of the filesystem hosted by the web server
* *Cross-site request forgery* - XSRF. An attack similar to XSS (cross site scripting) where the purpose is to trick the user or browser into performing actions they had not intended or would not have authorized

#### Assess and Mitigate Vulnerabilities in Mobile Systems

* Malicious insiders can bring in malicious code from outside, or exfiltrate information using mobile devices
* Eavesdropping is possible
* *Full device encryption* - Encrypt the entire device so that if it is lost, the data should be safe if the device is not unlocked
* *Remote wiping* - The ability to sanitize a device if it is lost or stolen, without having physical access to the device
* *Lockout* - When a user fails to provide their credentials after repeated attempts, the device may implement a cooldown period, or become locked forever
* *Screen locks* - Designed to prevent someone from casually picking up a device and using it
* *GPS* - Global Positioning System. Can be used to track the location of devices
* *Application control* - Device management solution that allows administrators to limit which applications can be installed on a device
* *Storage segmentation* - Artificially compartmentalizing types of data on a storage medium - ex. separating the device OS and installed apps
* *Asset tracking* - Management process used to maintain oversight over an inventory
* *Inventory control* - Hardware asset tracking, and the concept of using a mobile device as a means of tracking inventory in a warehouse
* *Mobile device management* - Software solution for managing mobile devices over a communications channel
* *Device access control* - Blocking unauthenticated access to a device
* *Removable storage* - Should also be encrypted, if allowed
* *Disabling unused features* - Remove apps and features that aren't needed for business tasks or common personal use
* *Key management* - Most crypto failures are from poor management, not poor algorithms. Have good key selection, based on quality random numbers.
* *Credential management* - Storage of credentials in a central location
* *Geotagging* - Using GPS to embed the location of a photo or other file
* *Application allow-listing* - Prohibiting unauthorized software from executing. Deny by default, implicit deny.
* *BYOD* - Bring your own device.
* *COPE* - Corporately owned, personally enabled.
* *CYOD* - Choose your own device.
* *Data ownership* - Commingling personal data and business data is likely to occur when using personal devices for business tasks, or vice versa.
  * Segmentation can help, isolation
* *Acceptable use policy* - Critical to define what is and is not acceptable usage while mixing personal activities and business tasks

#### Assess and Mitigate Vulnerabilities in Embedded Devices and Cyber-Physical Systems

* *Embedded system* - A computer implemented as part of a larger system, providing a limited set of specific functions related to the system itself
* *Static systems* - A set of conditions that don't change
* *Cyber-physical systems* - Offer computational means to control something in the physical world, often tied to IoT
* Security by:
  * *Network segmentation* - Keep these devices isolated from other systems
  * *Security layers* - Devices with different levels of sensitivity are grouped together and isolated
  * *Application firewalls* - Define a strict set of communication rules for a service and all users
  * *Manual updates* - Used in static environments to ensure that only tested updates, patches, authorized changes are implemented
  * *Firmware version control* - same as above, manual updates
  * *Wrappers* - Something used to enclose or contain something else, related to Trojan horse malware, but also encapsulation solutions
  * *Monitoring* - All devices must be monitored
  * *Control redundancy and diversity* - Especially for systems that are dangerous or whose outages may cause loss of life, you must be able to sustain an attack or outage that diminishes capacity

#### Essential Security Protection Mechanisms

* Software should not be trusted
* *Layering* - Implement a structure similar to a ring model
* *Abstraction* - Fundamental to object oriented programming, users of an object don't need to know the details of how the object works
* *Data hiding* - This is **different** from security by obscurity which is a bad practice. This is putting data in a location that it is not unnecessarily visible.
* *Process isolation* - Requires the OS to provide separate memory spaces for each process's instructions and data
* *Hardware segmentation* - Similar to process isolation in purpose, but for hardware

#### Security Policy and Computer Architecture

* *Principle of least privilege* - Discussed more in Chapter 13, users and resources should never have any more privileges than they need to do their assigned function. Avoid over-provisioning permissions.
* *Separation of privilege* - Builds on least privilege, using granular access permissions for each type of privileged operation so some can be assigned and others can be restricted - like separation of duties
* *Accountability* - You must be able to log everything and determine who or what is responsible for activities performed

#### Common Architecture Flaws and Security Issues

* *Covert channels* - A method that is used to pass information over a path that is not normally used for communication
  * *Covert timing channel* - Conveys information by altering the performance of a system component or modifying a resource's timing in a predictable manner - hard to detect
  * *Covert storage channel* - Conveys information by writing data to a common storage area where another process can read it
* *Attacks based on design or coding flaws and security issues* - See the OWASP section above
* *Trusted recovery* - Ensures all security controls remain in place in the event of a crash
* *Input and parameter checking* - Input sanitization, avoid buffer overflows, and many other issues addressed above
* *Maintenance hooks and privileged programs* - Entry points into a system that are known only by the developer of the system, also known as *back doors*
* *Incremental attacks* - Slow, gradual attack in increments
  * *Data diddling* - When an attacker gains access to a system and makes small, random, incremental changes to data during it's lifecycle rather than something big and obvious
  * *Salami attack* - Systemic whittling at assets in accounts or other records with financial value where small amounts are deducted from balances regularly
* *Timing, state changes, and communication disconnects* - Computers operate with precision and that's a weakness
  * *Time of check* - TOC, the time at which a subject checks the status of an object
  * *Time of use* - TOU, the time at which a subject uses an object
  * *TOCTTOU attack* - Time of check to time of use attack, replacing a data file after the identity has been verified, but before it has been used by a subject
* *Electromagnetic radiation* - EM radiation, reduce eminence through shielding
