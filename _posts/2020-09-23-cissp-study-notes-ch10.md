---
layout: post
title: CISSP Study Notes Chapter 10 - Physical Security Requirements
date: 2020-09-23 07:30
author: thmsrynr
comments: true
categories: [cissp, security, certifications]
---
Chapter 10 covers implementing site and facility security controls, designing sites and facilities, and generally protecting things from physical threats.

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

## Chapter 10: Physical Security Requirements

### My key takeaways and crucial points

#### Apply Security Principles to Site and Facility Design

* *Secure facility plan* - Outlines the security needs of your organization and emphasizes methods or mechanisms to employ to provide security
* *Critical path analysis* - Identifying relationships between mission-critical applications, processes, and operations
* *Technology convergence* - The tendency for various technologies, solutions, utilities, and systems to evolve and merge over time

#### Site Selection

* *Visibility* - Where are the closest emergency services located? Are there unique hazards? Locations of security cameras.
* Natural disasters
* *Facilities design* - Crime Prevention through Environmental Design (CPTED)

#### Implement Site and Facility Security Controls

* *Administrative physical security controls* - Include facility construction and selection, personnel controls, awareness training, emergency response
* *Technical physical security controls* - Include access controls, intrusion detection, alarms, monitoring, heating, ventilation, HVAC, power supplies, fire detection and suppression
* *Physical physical security controls* - Includes fences, lighting, locks, mantraps, dogs, guards
* Functional order controls should be used:
  1. Deterrence - Boundary restrictions
  1. Denial - Locked vault doors
  1. Detection - Using motion detectors
  1. Delay - Cable lock on a laptop

#### Equipment failure

* Service level agreements (SLA) - Defines vendor response time
* Mean time to failure (MTTF) - Expected typical functional lifetime of the device
* Mean time to repair (MTTR) - The average length of time required to perform a repair
* Mean time between failures (MTBF) - Estimation of the time between the first and any subsequent failures

### Wiring Closets

* An element of cable plant management policy
* *Entrance facility* - aka demarcation point, where the cable enters the building
* *Equipment room* - Main wiring closet
* *Backbone distribution system* - Between equipment room and telecommunication rooms
* *Telecommunications room* - Serves the connection needs of a floor or a section of a large building
* *Horizontal distribution system* - Between the telecommunication room and work areas

#### Server Room

* The more human incompatible a server room is, the more protection it offers against casual and determined attacks
* Walls should have one-hour minimum fire rating
* Datacenter could be a single tenant or multitenant
* *Smartcards* - Credit-card-sized, IDs, badges, security passes with an embedded magnetic strip, bar code, or integrated circuit chip
* *Memory cards* - Machine-readable ID cards with a magnetic strip
* *Proximity reader* - Passive device, a field-powered device, or a transponder
* *Passive device* - Like antitheft devices found in DVDs
* *Intrusion detection system* - Systems designed to detect a breach or attack
* *Masquerading* - Using someone else's security ID to gain entry into facilities
* *Piggybacking* - Following someone through a secured gate or doorway without being identified or authorized personally
* *Emanation* - Electromagnetic signals or radiation that can be intercepted by unauthorized individuals
* *Faraday cage* - An area designed with an external metal skin that surrounds the area on all sides and blocks electromagnetic interference (EMI)
* *White noise* - Random sounds, signal, or process that can drown out meaningful information
* *Control zone* - is an implementation of a Faraday cage or white noise generator or both to protect a specific area

#### Media storage facilities

* *Data remnants* - The remaining data elements left on a storage device after a standard deletion or formatting
* Have a librarian or custodian
* Implement drive sanitization or zeroization
* Verify data integrity with hash-based integrity checks
* Limit storage access, especially to evidence

#### Restricted and work area security

* *Shoulder surfing* - Gathering information from a system by observing the monitor or the use of the keyboard by the operator
* Sensitive Compartmented Information Facility (SCIF)

#### Utilities and HVAC Considerations

* *Uninterruptible power supply* - UPS. A type of self-charging battery that can be used to supply consistent clean power
* Line interactive UPS have surge protectors, voltage regulators
* *Fault* - Momentary loss of power
* *Blackout* - A complete loss of power
* *Sag* - Momentary low voltage
* *Brownout* - Prolonged low voltage
* *Spike* - Momentary high voltage
* *Surge* - Prolonged high voltage
* *Inrush* - Initial surge of power associated with connecting to a power source
* *Noise* - A steady interfering power disturbance or fluctuation
  * EMI - electromagnetic interference has two types
    * Common mode noise is generated by a difference in power between the hot and ground wires
    * Traverse mode noise is generated by a difference in power between the hot and neutral wires
  * Radio frequency interference - RFI, electrical appliances generate RFI like fluorescent lights
* *Transient* - A short duration of line noise
* *Clean* - Nonfluctuating pure power
* *Ground* - The wire in an electrical circuit that is grounded

#### Temperature, Humidity, and Static

* Humidity in a computer room should be maintained between 40-60%
* 1500 volts causes destruction of data stored on hard drives

#### Water Issues (e.g., Leakage, Flooding)

* Water and electricity don't mix

> This is seriously the only thing I have highlighted in this three paragraph section of the book

#### Fire Prevention, Detection, and Suppression

* **Protecting personnel from harm should always be the most important goal of any security or protection system**
* Fire extinguisher classes

| Class | Type | Suppression material |
|-|-|-|
| A | Common combustibles | Water, soda acid |
| B | Liquids | CO2, halon, soda acid |
| C | Electrical | CO2, halon |
| D | Metal | Dry powder |
| K | Kitchen (for grease fires, like B) | CO2, halon |

* *Fixed temperature detection* - Triggers suppression when a specific temperature is reached
* *Rate of rise detection* - Triggers detection if a temperature increases at a specific speed
* *Flame actuated system* - Triggers suppression based on infrared energy of flames
* *Smoke actuated system* - Uses photoelectric or radioactive ionization sensors
* Water suppression systems
  * *Wet pipe* - Always full of water
  * *Dry pipe* - Air escapes opening a water valve
  * *Deluge* - A form of dry pipe that uses larger pipes
  * *Preaction* - Combination of dry and wet pipe, system is dry until initial stages of fire when pipes are filled with water. Water is only released after sprinkler head activation triggers are melted by heat.
    * Most appropriate water-based system for environments with both humans and computers
* Water system failures are most often caused by human error
* Gas discharge systems
  * More effective than water discharge, but shouldn't be used where people are located
  * They deploy halon (not since it was banned), Co2, or FM-200 (halon replacement)

#### Implement and Manage Physical Security

* Fences 3-4 feet high deter casual trespassers
* Fences 6-7 feet high discourage most intruders except determined ones
* Fences 8 feet or more high with three strands of barbed wire deter even determined intruders
* *Gates* - Controlled exit and entry points in a fence
* *Turnstile* - Restricts movement in one direction
* *Mantrap* - A double set of doors that is often protected by a guard
* Perimeter protection needs lights with 2 foot-candles of power
* If a lighted area is 40 feet in diameter, poles should be 40 feet apart
  * 5 feet apart in parkades
* You need to be able to handle visitors
* *Lock* - A crude form of identification and authorization mechanism
* *Electronic access control lock* - Has an electromagnet to keep the door locked, a credential reader for authentication, and a sensor to reengage the electromagnet when the door is closed
* *Local alarm systems* - Must broadcast an audible alarm heard up to 400 feet away (up to 120 decibel)
* *Central station system* - Usually silent locally, but offsite monitoring agents are notified
* *Auxiliary station* - Emergency services are notified
* Closed circuit TV is not an automated detection and response system, it needs people watching it
* **Human safety is always the most important factor**
* Privacy means protecting personal information from discloser - NIST 800-122, GDPR
  * You are usually obliged to have physical security controls
