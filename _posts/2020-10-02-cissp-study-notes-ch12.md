---
layout: post
title: CISSP Study Notes Chapter 12 - Secure Communications and Network Attacks
date: 2020-09-30 07:30
author: thmsrynr
comments: true
categories: [cissp, security, certifications]
---
Chapter 12 gets into implementing secure communications channels according to design for voice, multimedia, remote access, data communications, and virtualized networks.

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

## Chapter 12: Secure Communications and Network Attacks

### My key takeaways and crucial points

#### Secure Communications Protocols

* IPSec
  * VPNs
  * Either transport or tunnel mode
* Kerberos
  * Single sign on solution for users and provides protection for logon credentials
* SSH
  * End to end encryption
* Signal Protocol
  * End to end encryption for voice communications, videoconferencing, and text message services
* Secure Sockets Layer - SSL
  * Session oriented protocol that provides confidentiality and integrity
  * Superseded by TLS

#### Authentication Protocols

* Challenge Handshape Authentication Protocol (CHAP)
  * Encrypts usernames and passwords
* Password Authentication Protocol (PAP)
  * Transmits usernames and passwords in cleartext
* Extensible Authentication Protocol (EAP)
  * Customized authentication security solutions
* Protected Extensible Authentication Protocol (PEAP)
  * Encapsulates EAP in a TLS tunnel

#### Voice over Internet Protocol (VOIP)

* VOIP
  * Encapsulates audio into IP packets to support telephone calls over TCP/IP
* *Vishing* is VoIP phishing

#### Social Engineering

* *Social engineering* - The means by which an unauthorized person gains access or the trust of someone inside your organization
* Always err on the side of caution
* Always request proof of identity
* Require callback authorization on voice-only requests
* Classify information properly
* Have a company security policy that is known by employees
* Offer secure disposal or destruction for sensitive materials

#### Fraud and Abuse

* *Phreakers* - Attack phone systems like attackers abuse computer networks
* Restrict dial in and dial out features
* Define an acceptable use policy
* Deploy Direct Inward System Access (DISA)
* Telephone attack tools
  * Black boxes
    * Manipulate line voltages to steal long distance services
  * Red boxes
    * Simulate tones of coins being deposited into a pay phone
    * Just a tape recorder
  * Blue boxes
    * Simulate 2600 Hz tones to interact directly with telephone network trunk systems
  * White boxes
    * Control the phone system with a keypad

#### Manage Email Security

* X.400 standard for addressing and message handling
* *Sendmail* is most common SMTP for Unix systems
* *Exchange* is most common SMTP for Windows systems
* Avoid turning SMTP server into an *open relay*
  * SMTP server that does not authenticate senders
* Email security goals
  * Nonrepudiation
  * Privacy, confidentiality
  * Message integrity
  * Classify sensitive content
* Email security issues
  * Often plaintext
  * Common delivery mechanism for viruses
  * Spoofing source addresses is simple
  * Denial of service attacks
* Email security solutions
  * Secure Multipurpose Internet Mail Extensions (S/MIME)
    * X.509 certificates
  * Pretty Good Privacy (PGP)
    * Independently developed
  * Opportunistic TLS
* Fax security
  * Fax encryption, link encryption, activity logs, exception reports
  * Disable automatic printing

#### Remote Access Security Management

* Scraping
  * Automated tool interacts with a human interface
* Authentication protection matters
  * PAP, CHAP, EAP, PEAP, RADIUS, TACAS+
* Use callback and caller ID
* Dial Up Protocols
  * Point to Point Protocol (PPP)
    * Full-duplex
  * Serial Line Internet Protocol (SLIP)
    * Older technology
* Centralized remote authentication services
  * Remote Authentication Dial In User Service (RADIUS)
    * Centralizes authentication of remote connections
  * Terminal Access Controller Access-Control System (TACACS+)
    * Improves XTACACS by adding two factor authentication
    * Not backwards compatible

#### Virtual Private Network

* VPN is a communication tunnel
* Tunneling
  * Network communications process that protects the contents of protocol packets by encapsulating them in packets of another protocol
  * Can be used if the primary protocol is not routable
* Can connect two individual systems, or two entire networks
* Common Protocols
  * PPTP, L2F, L2TP operate on data link layer
  * PPTP, IPSec are limited for use on IP networks
* Point to Point Tunneling Protocol (PPTP)
  * Initial tunnel negotiation process is not encrypted
* Layer 2 Forwarding Protocol (L2F) & Layer 2 Tunneling Protocol (L2TP)
  * Cisco proprietary
  * Not encrypted (L2F)
  * L2TP combines elements from PPTP and L2F, supports TACACS+ and RADIUS
* IP Security Protocol
  * Authentication Header (AH)
    * Provides authentication, integrity, nonrepudiation
  * Encapsulating Security Payload (ESP)
    * Provides encryption to protect the confidentiality of transmitted data, but can also perform limited authentication
    * In tunnel mode, the entire IP packet is encrypted

#### Virtual LAN

* Hardware imposed network segmentation, created by switches
* Used for traffic management
* Used to isolate traffic between network segments
* Deny by default, allow by exception
* *Broadcast storm* - A flood of unwanted Ethernet broadcast network traffic

#### Virtualization

* Indistinguishable from traditional servers and services from a user's perspective
* Virtual Software
  * Virtual applications/Containers are software products deployed in a way that it is fooled into believing it is interacting with a full host OS
* Virtual Networking
  * Software defined networking (SDN)
  * Effectively network virtualization

#### Network Address Translation

* Private IP addresses are defined in RFC 1918
* Most networks employ NAT
* Private IP Addresses
  * 10.0.0.0 - 10.255.255.255 (Class A range)
  * 172.16.0.0 - 182.31.255.255 (Class B range)
  * 192.168.0.0 - 192.168.255.255 (Class C range)
* Stateful NAT
  * Maintains a mapping between requests made by internal clients, a client's internal IP address, and the IP address of the internet service contacted
  * Maintains information about the communication sessions between clients and external systems
* Static NAT
  * Specific internal client IP addresses are assigned in a permanent mapping
* Dynamic NAT
  * Multiple internal clients access to a few leased public IPs
* Not directly compatible with IPSec, but there are versions that do work

#### Automatic Private IP Addressing

* Automatic Private IP Addressing (APIPA)
  * If DHCP fails to assign an address, this Windows feature assigns an address between 162.254.0.1 to 169.254.255.254, and a class B subnet mask
* You should be able to convert a 32 bit binary number to a single decimal number
* RFC 1918 covers loopback addresses
  * 127.x.x.x
  * Usually only 127.0.0.1 is used

#### Circuit Switching

* Dedicated physical pathway
* Pathway is permanent throughout a single conversation

#### Packet Switching

* When the message or communication is broken up into small segments and sent across intermediary networks to the destination
* Does not enforce exclusivity of communication pathways
* Circuit switching vs Packet switching

|Circuit Switching|Packet Switching|
|-|-|
|Constant traffic|Burst traffic|
|Fixed known delays|Variable delays|
|Connection oriented|Connectionless|
|Sensitive to connection loss|Sensitive to data loss|
|Used primarily for voice|Used for any type of traffic|

#### Virtual Circuits

* Private Virtual Circuits are like a dedicated leased line
  * Like a two way radio, or walkie talkie
* Switched Virtual Circuits are like dial up connections because a virtual circuit has to be created using best paths available before it can be used
  * More like shortwave, or ham radio

#### WAN Technologies

* Dedicated line is also known as leased line or point to point link
* Nondedicated line requires a connection to be established before data transmission can occur
* X25 WAN Connections
  * Predecessor to Frame Relay
* Frame Relay
  * Supports multiple PVCs over a single WAN carrier service connection
  * Committed information rate - guaranteed min bandwidth a customer receives
  * Requires a DTE/DCE at each connection point
* ATM
  * Asynchronous Transfer Mode
  * Fragments communications into fixed length 53 byte cells
  * Very efficient, high throughput
* Synchronous Digital Hierarchy and Synchronous Optical Network
  * SDH and SONET
  * Fiber optic high speed networking standards

#### Miscellaneous Security Control Characteristics

* Transparency
  * The characteristic of a service, control, or access mechanism that ensures that it is unseen by users
* Verify integrity
  * Uses a checksum, called a hash total
* Transmission mechanisms
  * Error correction
  * Retransmission

#### Security Boundaries

* A line of intersection between any two areas, subnets, or environments that have different security requirements or needs
* Exist between physical environment and logical environment
* Ex: A perimeter between a protected area and an unprotected one

#### Prevent or Mitigate Network Attacks

* DoS and DDoS
  * Resource consumption attacks
  * Two types
    * Exploiting vulnerability in hardware or software
    * Flood the victim's communication pipeline
  * Attackers may use *bots* (aka *zombies*, *agents*) onto unwitting systems and use them to participate in traffic flooding
  * Collections of bots are called *botnets*
* Eavesdropping
  * Listening to communication traffic
* Impersonation/Masquerading
  * Pretending to be someone or something you are not, in order to gain unauthorized access to a system
  * Different from spoofing, where an entity puts forth a false identity but without any proof
* Replay attacks
  * Replaying captured traffic against a system
* Modification attacks
  * Captured packets are altered
* Address Resolution Protocol Spoofing
  * Provides false MAC addresses for requested IP address
  * Facilitates man in the middle attacks
* DNS poisoning, spoofing, hijacking
  * Poisoning and spoofing are known as resolution attacks - when an attacker alters the domain name to IP address mappings to redirect traffic to a rogue system
  * Homograph attacks - Register phony international domain names, letters in Cyrillic
* Hyperlink spoofing
  * Used to redirect traffic to a rogue system, or simply to divert traffic away from it's intended destination
  * Alteration of hyperlink URLs in HTML code
* Related to phishing is pretexting, where one obtains personal information under false pretenses
