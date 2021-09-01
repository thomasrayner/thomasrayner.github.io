---
layout: post
title: CISSP Study Notes Chapter 18 - Disaster Recovery Planning
date: 2021-09-01 07:30
author: thmsrynr
comments: true
categories: [cissp, security, certifications]
---
Chapter 18 dives into security assessment and testing, and security operations like implementing recovery strategies, DR processes, and testing disaster recovery plans.

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

## Chapter 18 - Disaster Recovery Planning

### My key takeaways and crucial points

#### Managing Incident Response

* *Disaster recovery plan* - covers situations where tensions are already high and cooler heads may not naturally prevail, should be setup to basically run on autopilot and remove all decision making.
* Natural disasters
  * Earthquake - shifting of seismic plates
  * Floods - Gradual accumulation of rainwater, or caused by seismic activity (tsunamis)
    * "100 year flood plain" means there is an estimated chance of flooding in any give year of 1/100
  * Storms - Prolonged periods of intense rainfall
  * Fires - including wildfires, and man-made, may be caused by carelessness, faulty electrical wiring, improper fire proteciton practices
    * 1000 building fires in the United States every day
  * Acts of terrorism - General business insurance may not cover against terrorism
  * Bombings/explosions - Including gases from leaks
  * Power outages - protected against by uninterruptible power supply (UPS)
  * Network, utility, and infrastructure failures
    * Which critical systems rely on water, sewers, natural gas, or other utilities?
    * Think about internet connectivity as a utility.
    * Do you consider people a critical business system? People rely on things like water.
  * Hardware/software failures - Hardware components simply wear out, or suffer physical damage.
  * Strikes/picketing - human factor. If a large number of employees walk out at the same time, what would happen to your business?
  * Theft/vandalism - Insurance provides some financial protection

#### Understand System Resilience and Fault Tolerance

* *Single point of failure* - SPOF, any component that can cause an entire system to fail.
* *Fault tolerance* - the ability of a system to suffer a fault but continue to operate
* *System resilience* - the ability of a system to maintain an acceptable level of service during an adverse event
* Protecting hard drives
  * RAID-0 - striping
  * RAID-1 - mirroring
  * RAID-5 - striping with parity
  * RAID-10 - aka RAID-1+0, or a stripe of mirrors
* Protecting servers
  * *Failover* - If one server fails, another server in a cluster can take over its load
  * Load balancers detect failures and stop sending traffic to the bad server
  * Provide fault tolerance
  * Many IaaS providers offer load balancing that automatically scales resources as needed
* Protecting power sources
  * *Uninterruptible power supply* - UPS, battery supplied power for a short period of time that kicks in when power is lost, while a generator starts up to provide backup power
  * *Spike* - a quick instance of voltage increase
  * *Sag* - a quick reduction in voltage
  * *Surge* - a long instance of a spike
  * *Brownout* - a long instance of a sag
  * *Transients* - noise on a power line that can come from different sources
  * *Line interactive UPS* - include variable voltage transformer that helps adjust to over/under voltage events
  
#### Trusted Recovery

* *Trusted recovery* - After a failure, the system is just as secure as it was before
* *Fail-secure system* - defaults to a secure state in the event of a failure, blocking all access
  * Firewalls are normally fail-secure
* *Fail-open system* - defaults to an open state, granting access
  * Emergency exit doors are normally fail-open to allow people to escape a hazard in an emergency
* *Manual recovery* - After a system failure, it does not fail in a secure state and an administrator needs to perform actions to implement a secured or trusted recovery
* *Automated recovery* - The system can perform a trusted recovery to restore itself against at least one type of failure
* *Automated recovery without undue loss* - Like automated recovery but it also includes mechanisms to ensure that specific objects are protected to prevent their loss
* *Function recovery* - Automatically recover specific functions

#### Quality of Service

* *Bandwidth* - network capacity
* *Latency* - time it takes a patcket to travel
* *Jitter* - variation in latency
* *Packet loss* - requires retransmission
* *Interference* - electrical noise, faulty equipment

#### Recovery Strategy

* DR plan should be designed so first employees on the scene can immediately start recovery efforts in an organized way, even if official disaster ecovery team isn't there yet
* Insurance can reduce the risk of financial losses
* Business unit and functional priorities
  * Must engineer DR plan to allow highest priority business units to recover first
  * Not all critical functions will be carried out in critical business units
  * Perform a business impact assessment (BIA) - Identify vulnerabilities, develop strategies to minimize risk, provide a report that describes risks. Also identify costs related to failures. Results in a prioritization task. Minimum output of BIA is a simple listing of business units in priority order.
* Crisis management
  * Individuals in business who are most likely to notice an emergency situation should be trained in DR procedures and know proper notification processes
* Emergency communications
  * Communicate internally during a disaster so employees know what is expected of them
* Workgroup recovery
  * The goal is to restore workgroups to the point that they can resume their activities in their usual work locations
  * May need separate recovery facilities for different workgroups
* Alternate processing sites
  * *Cold site* - standby facility, no computing facilities preinstalled. Low cost.
  * *Hot site* - backup facility that is maintained in constant working order, can have replication forced to it or backups taken from primary site to hot site. Higher cost.
  * *Warm site* - between hot and cold sites, contain equipment needed to establish operation, but not the production data, may take 12 hours to become operational.
  * *Mobile site* - self contained trailers or other relocated units
  * *Service bureau* - company that leases computer time
  * *Cloud computing* - ready-to-run images in cloud providers is usually cost-effective
  * *Mutual assistance agreements* - MAA, aka reciprocal agreements are rarely implemented but would mean two organizations pledge to assist each other if there's a disaster by sharing computing facilities. Difficult to enforce, confidentiality concerns, proximity is an issue.
* Database recovery
  * *Electronic vaulting* - database backups are moved to a remote site using bult transfers. Done in batch, not realtime.
  * *Remote journaling* - data transfers are performed in a more expeditious mannar, still in bulk transfer, but done in realtime.
  * *Remote mirroring* - most advanced, most expensive. Live DB server is maintained at the backup site.

#### Recovery Plan Development

* Maintain multiple types of plan documents for different audiences
* Checklists
* Emergency response - simple but comprehensive instructions for essential personnel to follow immediately upon recognizing that a disaster is in progress. Most important tasks first.
* Personnel and communications - List of personnel to contact in the event of a disaster
* Backups and offsite storage
  * *Full backups* - complete copy
  * *Incremental backups* - Files that have been modified since most recent full or incremental backup. Only files with archive bit turned on are duplicated, then those vits are turned off.
  * *Differential backups* - Files that have been modified since the last full backup. Only files with archive bit turned on, but the bit is left on afterwards.
  * Difference between incremental and differential is the time needed to restored data in an emergency vs time taken to create the backups.
* *Software escrow arrangement* - protects a company against failure of a developer to provide adequate support for products or if the developer goes out of business
* External communications may be performed by public relations officials
* Logistics refers the problem of moving large numbers of people, equipment, and supplies
* Recovery is bringing business operations and processes back to a working state, while restoration involves bringing the facility and environment back to a working state. DRP should define criteria for both.

#### Training, Awareness, and Documentation

* Should have these elements
  * Orientation training for new employees
  * Initial training on new DR roles
  * Detailed refersher training for DR team members
  * Awareness refershers for all other employees
* DRP should be treated as exteremely sensitive and provided to individuals on a compartmentalized, need-to-know basis

#### Testing and Maintenance

* *Read through test* - Distribute copies of DR plans and review them
* *Structured walk through* - Table-top exercise with the members of the DR team gather, basically role-playing
* *Simulation test* - Team members are presented with a scenario and asked to develop a response
* *Parallel test* - Relocating personnel to alternate recovery site and implementing site activation procedures
* *Full-interruption test* - Actually shut down the primary site and shift them to the backup site
* DR plans are living documents and need maintenance. They should refer to the organization's business continuity plan as a template.
