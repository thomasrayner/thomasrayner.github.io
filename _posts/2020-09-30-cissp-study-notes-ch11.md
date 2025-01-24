---
layout: post
title: CISSP Study Notes Chapter 11 - Secure Network Architecture and Securing Network Components
date: 2020-09-30 07:30
author: thmsrynr
comments: true
categories: [cissp, security, certifications]
---
Chapter 11 goes over a lot of networking topics including the OSI and TCP/IP models, IP networking, multilayer protocols, converged protocols, software-defined networks, wireless networks, and a whole bunch of hardware items.

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

## Chapter 11: Secure Network Architecture and Securing Network Components

### My key takeaways and crucial points

#### OSI Model

* Know the different levels of the OSI model in order
  * Application (7)
  * Presentation
  * Session
  * Transport
  * Network
  * Data Link
  * Physical (1)
  * Come up with a pneumonic device to remember them if you have to - All People Seem To Need Data Processing, for instance
* *Encapsulation/Deencapsulation* - The addition of a header and maybe a footer to the data received by each layer from the layer above it before it's handed off to the layer below, and then the subsequent removal of those headers and footers and the received data flows back up the OSI model on the other end.
* Pieces of data have different names at different points in the OSI model
  * *Protocol data unit* - PDU. Application, presentation, session layer data units.
  * *Segment* or *datagram* - Transport layer data units.
  * *Packet* - Network layer.
  * *Frame* - Data link layer.
  * *Bits* - Physical layer.

#### Physical Layer

* Converts the frame into bits for transmission over the physical connection medium

#### Data Link Layer

* Formatting the packet from the network layer into the proper format for transmission
* Ethernet - 802.3
* Asynchronous Transfer Mode - ATM
* Fiber Distributed Data Interface - FDDI
* Address Resolution Protocol - ARP - Used to resolve IP addresses into MAC addresses
* Layer 2 Tunneling Protocol - L2TP
* *Media Access Control address* - MAC address, 48 bit binary address that identifies a device
  * First 3 bytes of the address denotes the vendor or manufacturer of the physical network interface
* Data link layer has two sub-layers
  * Logical Link Control - LLC
  * MAC

#### Network Layer

* Adding routing and addressing information to data
* Internet Group management Protocol (IGMP) - Multicast protocol
* The three most recognized non-IP protocols are IPX, AppleTalk, and NetBEUI
* Routers and bridge routers function at layer 3
* Routing protocols
  * *Distance vector* - keep a list of destination networks along with metrics of direction and distance measured in hops
  * *Link state* - keep a topography map of all connected networks and use this map to determine the shortest path to a destination network

#### Transport Layer

* Manages the integrity of a connection and controls the session
* Transmission Control Protocol - TCP
* User Datagram Protocol - UDP
* Secure Sockets Layer - SSL
* Transport Layer Security - TLS

#### Session Layer

* Establishes, maintains, terminates communication sessions between two computers
* Network File System - NFS
* Structured Query language - SQL
* Remote Procedure Call - RPC
* Simplex - One way communication
* Half-Duplex - Two way communication, one direction at a time
* Full-Duplex - Two way communication, two directions at the same time

#### Presentation Layer

* Transforms data from the application layer into a format that any system using the OSI model can understand
* Images, video, sound, ASCII, JPEG, etc.

#### Application Layer

* Interfacing user applications, network services, or the OS with the protocol stack
* The application is not located at this layer

#### TCP/IP Model

* AKA the DARPA or DOD model
* Only has four layers
  * Application - aka Process, maps to OSI Application, Presentation, Session layers
  * Transport - aka Host-To-Host, maps to OSI Transport layer
  * Internet - aka Internetworking, maps to OSI Network layer
  * Link - aka Network Access, maps to OSI Data Link, Physical layers
* Can be secured using VPN - virtual private network
  * L2TP, SSH, SSL/TLS VPNs, IPSec
  * *TCP wrappers* - Applications that can serve as a basic firewall by restricting access to ports and resources based on user IDs or system IDs

#### Transport Layer Protocols

* Ports 0 through 65535
  * Well known ports: 0 - 1023
  * Registered ports: 1024 - 49151
  * Random, dynamic, ephemeral ports: 49152 - 65535
* *Transport Control Protocol* - TCP
  * Connection oriented
  * Reliable sessions
  * Handshake process
    * Client sends a SYN packet to server
    * Server responds with SYN/ACK to client
    * Client responds with ACK to server
  * Uses FIN packets to terminate connections
  * Uses ACK packets to confirm that data has been received
  * Uses RST packets to forcibly close connections
  * Uses a graceful 4 packet teardown
    * Each side sends a FIN
    * Each side ACKs the FIN sent by the other
  * IP protocol header field value for TCP is 6
* *User Datagram Protocol* - UDP
  * Connectionless, best effort
  * Considered unreliable

#### Network Layer Protocols and IP Networking Basics

* IP provides route addressing for data packets, provides a means of identity and prescribes transmission paths
* IPv4 vs IPv6 - v4 uses 32 bit addresses, v6 uses 128 bits
* IP classes

|Class|First binary digits|Decimal range of first octet|Default subnet mask|CIDR equivalent|
|-|-|-|-|-|
|A|0|1-126|255.0.0.0|/8|
|B|10|128-191|255.255.0.0|/16|
|C|110|192-223|255.255.255.0|/24|
|D|1110|225-239|
|E|1111|240-255|

* Class A network starting with 127 is set aside for loopback address
* *Classless Inter-Domain Routing* - CIDR, represents subnet mask as a slash and the number of mask bits instead of the full dotted-decimal mask notation
* *Internet Message Control Protocol* - ICMP
  * Used to determine the health of a network or link
  * *Denial of service* - DOS, a type of attack sometimes associated with ICMP - specifically ping of death, smurf attacks, and ping floods
  * ICMP type field values
    * 0 - Echo reply
    * 3 - Destination unreachable
    * 11 - Time exceeded
* *Internet Group Management Protocol* - IGMP, allows systems to support multicasting
* *Address Resolution Protocol* - ARP, used to resolve IP addresses into MAC addresses
  * Uses caching and broadcasting

#### Common Application Layer Protocols

* *Telnet* - TCP port 23, terminal emulation
* *File Transfer Protocol* - FTP TCP port 20 (passive data) and 21 (control connection) for exchanging files
* *Trivial File Transfer Protocol* - TCP TFTP port 69
* *Simple Mail Transfer Protocol* - SMTP TCP port 25, for transmitting email messages
  * POP3, TCP port 110
  * IMAP, TCP port 143
* *Dynamic Host Configuration Protocol* - DHCP UDP port 67 & 68, used to assign IP addresses and configuration settings to systems on bootup
* *Hypertext Transfer Protocol* - HTTP TCP port 80, used to transmit web page elements
* *Secure Sockets Layer* - SSL TCP port 443, adds a security protocol at the Transport layer to HTTP (making it HTTPS)
* *Line Print Daemon* - LPD TCP port 515, spool print jobs
* *X Window* - TCP port 6000-6063, GUI API for CLI OS
* *Network File System* - NFS TCP port 2049
* *Simple Network Management Protocol* - SNMP UDP port 161, port 162 for trap messages, network service to collect network health and status information
* DNS port 53
* Kerberos port 88
* L2TP port 1701
* PPTP port 1723
* RDP port 3389
* TCP/IP is considered a *multilayer protocol* because it is made up of many different protocols spread across multiple layers of the stack

#### DNP3

* Distributed Network Protocol is primarily used in electric and water utility management industries
* Used with SCADA

#### TCP/IP Vulnerabilities

* SYN flood attacks
* Spoofing
* Man in the middle
* Hijack
* *Packet Sniffing* - Capturing packets from the network in hopes of extracting useful information from the contents of the packet

#### Domain Name System (DNS)

* *Top level domain* - TLD, the `.ca` in www.thomasrayner.ca
* *Registered domain name* - The `thomasrayner` in www.thomasrayner.ca
* *Subdomain or hostname* - The `www` in www.thomasrayner.ca
* *Primary authoritative name server* - Hosts the original zone file for the domain
* *Secondary authoritative name server* - Used to host read-only copies of the zone file
* *Zone file* - Collection of *resource records* or details about the specific domain
* *DNSSEC* provides reliable authentication between devices during DNS operations
* *DNS Poisoning* - Falsifying the DNS information used by a client to reach a desired system
  * Involves attacking the real DNS server and placing incorrect information into its zone file
* *Rogue DNS server* - AKA DNS Spoofing, Pharming
* *Pharming* - malicious redirection of a valid website's URL or IP address to a fake website that hosts a false version of the original valid site
* *Domain hijacking* - Changing the registration of a domain name without the authorization of the valid owner

#### Converged Protocols

* *Converged Protocols* - Merging of specialty protocols with standard protocols
* *Fiber Channel over Ethernet* - FCoE, for Storage Area Networks, or Network Attached Storage
* *Multiprotocol Label Switching* - MPLS, Directs data across a network based on short path labels rather than longer network addresses
* *Internet Small Computer System Interface* - iSCSI, Enables location independent file storage, transmission and retrieval over networks, low cost alternative to Fiber Channel
* *Voice over IP* - VoIP, Transports voice and/or data over a TCP/IP network
* *Software Defined Networking* - SDN, Complexities of a traditional network often forces an organization to stick with a single device vendor, so SDN offers a net network design that is programmable from a central location

#### Content Distribution Networks

* *Content Distribution Networks* - CDNs, a collection of resource services deployed in numerous data centers across the internet in order to provide low latency, high performance, and high availability of the hosted content

#### Wireless Networks

* *Data emanation* - Transmission of data across electromagnetic signals
* Emanations occur whenever electrons move

#### Securing Wireless Access Points

* *Wireless cells* - Areas within a physical environment where a wireless device can connect to an access point
* 802.11 is the IEEE standard for wireless network communications
  * 802.11i - Security standard
* *Ad hoc mode* - Any two wireless devices can communicate without centralized control authority
  * *Infrastructure mode* requires a wireless access point
* *Stand alone mode* - When there is a wireless access point connecting clients to each other but not to any wired resources
* *Wired extension mode* - When access points act as a connection point to wired networks
* *Service Set Identifier* - SSID, the name of a wireless network when a WAP is used
* *Channels* - Subdivisions of wireless frequencies

#### Securing the SSID

* SSID is broadcast by the WAP using *beacon frames*
* Hiding the SSID is not true security, because it is easily discoverable
* *Site survey* - The process of investigating the presence, strength, and reach of WAPs deployed

#### WEP

* *Wired Equivalent Privacy* - WEP
* Uses a predefined shared secret key
* Key is static and shared among all WAPs and devices
* Was cracked almost as soon as it was released
* Uses Rivest Cipher 4 (RC4)
* Weaknesses: static common key, and poor implementation of IVs (initiation vectors)

#### WPA

* *WiFi Protected Access* - WPA
* RSN - Robust Secure Network
* Based on LEAP and Temporal Key Integrity Protocol (TKIP)
* Use of a single static passphrase is the downfall of WPA
* LEAP and TKIP encryption options are now crackable

#### WPA2

* Full 802.11i implementation
* Based on AES encryption

#### 802.1X/EAP

* Standard port-based network access control, ensures that clients cannot communicate until proper authentication has taken place
* Uses RADIUS or TACAVS, certs, smart cards, etc.
* *Extensible Authentication Protocol* - EAP, not a specific mechanism of authentication

#### PEAP

* Protected Extensible Authentication Protocol
* EAP methods within a TLS tunnel

#### LEAP

* Lightweight EAP
* Cisco proprietary
* Should be avoided when possible

#### MAC Filter

* A list of authorized wireless client interface MAC addresses
* Blocks access to nonauthorized devices

#### TKIP

* Temporal Key Integrity Protocol
* Improvements include key-mixing function that combines with the initialization vector with the secret root key before using RC4 to perform encryption
* Prevents replay attacks

#### Antenna Types

* *Omnidirectional* - Can send and receive signals in all directions
* *Directional* - Can send and receive in only one direction

#### WPS

* WiFi Protected Setup
* Simplifies the effort involved with adding new clients to a well secured wireless network
* Generally recommended to leave this turned off

#### Captive Portals

* An authentication technique that redirects a newly connected wireless client to a portal access control page

#### General WiFi Security Procedure

* Treat wireless as remote access
* Treat wireless as external access

#### Wireless Attacks

* *War driving* - Looking for wireless networks they aren't authorized to access
* *War chalking* - Physically marking an area with information about the presence of a wireless network
* *Replay* - Retransmission of captured communications
* *IV* - Initialization vector, a mathematical and crypto term for a random number, becomes a point of weakness when it's too short, exchanged in plaintext, or selected improperly
* *Rogue access points* - May be planted by an employee for convenience, or by an attacker
* *Evil twin* - When a hacker operates a false access point that will automatically clone an access point based on a client's request to connect
  * Eavesdrops on the wireless signal for reconnect requests and spoofs it's identity and offers a plaintext connection to the client

#### Secure Network Components

* *Intranet* - Private network, internal
* *Extranet* - Cross between internet and intranet
* *Demilitarized zone* - DMZ, extranet for public consumption
* *Network access control* - Controlling access to an environment
  * Prevent/reduce zero day attacks
  * Enforce security policy
  * Use identities to perform access control
* Firewalls filter traffic
  * Most effective against unrequested traffic and attempts to connect from outside the private network
  * Typically block viruses or malicious code
  * Static packet filtering firewalls filter traffic by examining message headers
  * Application gateway level firewalls are also called proxies, and are mechanisms that copy packets from one network to another
  * Circuit level gateway firewalls establish communication sessions between trusted partners
  * Stateful inspection firewalls, aka dynamic packet filtering, evaluate the state or the context of network traffic
  * Deep packet inspection firewalls filter the payload contents of a communication rather than only basing filtering on header values
  * Next gen firewalls are also composed of intrusion prevention systems, proxies, quality of service management, and more
  * Multihomed firewalls have at least two interfaces to filter traffic between two networks

#### Endpoint Security

* Each individual device must maintain local security
* *Collision domain* - A group of networked systems, and two or more systems may transmit simultaneously
* *Broadcast domain* - A group of networked systems, and all members receive a broadcast signal when one member transmits it
* Repeaters, concentrators, and amplifiers strengthen communication signals
* Hubs are multiport repeaters
* Modems are used for accessing the PSTN (publicly switched telephone network)
* Bridges connect two networks together
* Switches are intelligent hubs that know the addresses of systems connected to each outbound port
  * Can implement VLANs
* Routers control traffic flow on networks
* Brouters are combinations of routers and bridges, and connect systems using the same protocols
* Gateways connect networks that are using different network protocols
* Proxies are a form of gateway that does not translate across protocols

#### Cabling, Wireless, Topology, Communications, and Transmission Media Technology

* Coaxial cable
  * 10Base2 aka thinnet spans distances up to 185 meters and provides up to 10 Mbps
  * 10Base5 aka thicknet spans up to 500 meters and provides 10 Mbps
* Broadband and baseband
  * Baseband cables can only transmit a single signal at a time
  * Broadband cables can transmit multiple signals simultaneously
* Twisted pair
  * STP (shielded)
  * UTP (unshielded)
  * Crosstalk occurs when data transmitted over one set of wires is picked up by another set of wires due to radiating electromagnetic fields produced by the electrical current
  * Cat 5 - 100 Mbps
  * Cat 6 - 1000 Mbps
  * Cat 5e is enhanced Cat 5 designed to protect against crosstalk
* Plenum cable is sheathed with special material that does not release toxic fumes when burned, must be used to comply with building codes

#### Network Topologies

* *Ring* - Each system is a point on a circle
* *Bus* - Trunk or backbone, linear or a tree
* *Star* - Centralized connection device
* *Mesh* - Using numerous paths to connect each system to all other systems

#### General Wireless Concepts

* Spread spectrum means communication occurs over multiple frequencies
* Orthogonal frequency division multiplexing
  * Modulated signals are perpendicular and thus do not cause interference with each other
  * Ultimately OFDM requires a smaller frequency set but offers greater data throughput
* Bluetooth (802.15)
  * Personal area network (PAN)
  * 2.4 GHz frequencies
  * *Bluejacking* - Allows an attacker to transmit short messages to your device
  * *Bluesnarfing* - Allows hackers to connect with your devices without your knowledge
  * *Bluebugging* - Remote control over the feature and functions of a Bluetooth device
  * Typically a range of 30 - 100 feet
* RFID
  * Radio frequency identification
  * Current generated in an antenna when placed in a magnetic field
* NFC
  * Near field communication
  * Derivative of RFID
* Mobile devices
  * Keep nonessential information off portable devices
  * Keep systems locked and encrypted when possible

#### LAN Technologies

* *Ethernet* - Shared media LAN technology
  * IEEE 802.3
  * Individual units of Ethernet data are called Frames
* *Token Ring* - Token passing mechanism to control which system scan transmit data over the network medium
* *Fiber distributed data interface* - FDDI, high speed token passing technology. Copper Distributed Data Interface uses twisted pair cables.
* Digital signals are more reliable than analog signals over long distances or when interference is present
* *Synchronous communications* - Rely on timing or clocking mechanisms
* *Asynchronous communications* - Rely on a stop and start delimiter bit
* *Broadcast* - Communication to all recipients
* *Multicast* - Communication to multiple specific recipients
* *Unicast* - Communication to one specific recipient
* *Carrier sense multiple access with collision avoidance* - CSMA
  * Performs collision avoidance on LAN media access technologies
  * *CA mode* is used on 802.11 wireless networks and AppleTalk, attempts to avoid collisions by granting only a single permission to communicate at a time
  * *CD mode* is used by Ethernet networks and responds to collisions by having each member of a collision domain wait for a short but random period of time before starting over
