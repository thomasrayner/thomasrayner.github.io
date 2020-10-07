---
layout: post
title: CISSP Study Notes Chapter 15 - Security Assessment and Testing
date: 2020-10-07 07:30
author: thmsrynr
comments: true
categories: [cissp, security, certifications]
---
Chapter 15 is a hefty chapter which covers designing and validating assessment, test, and audit strategies, conducting security control testing, collecting security process data, and then analyzing test output, and conducting security audits.

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

## Chapter 15: Security Assessment and Testing

### My key takeaways and crucial points

#### Security Testing

* Security tests
  * Verify that a control is functioning properly
* Frequent automated tests supplemented by infrequent manual tests are recommended
  * Review the results of those tests to ensure that each test was successful

#### Security Assessments

* Security assessment
  * Comprehensive reviews of the security of a system applications, or other tested environment
* Information security professional performs a risk assessment
* Assessment report addressed to management

#### Security Audits

* Security audit
  * Use many of the same techniques for assessments, but must be performed by independent auditors
* Assessments are internal use only
* Audits are done for the purpose of demonstrating the effectiveness of controls to a third party
* Internal audits
  * Intended for internal audiences
* External audits
  * Performed by outside auditing firms
* Third party audits
  * Conducted by, or on behalf of, another organization
  * Type I
    * Controls provided by audited organization as well as auditor opinion based on description
  * Type II
    * Minimum six month period and also include an opinion from the auditor
    * Considered more reliable
* Auditing standards
  * COBIT
    * Describes common requirements orgs should have in place surrounding information systems
  * ISO 27001
    * A standard approach for setting up an information security management protocol
    * ISO 27002 goes into more detail

#### Describing Vulnerabilities

* Common vulnerabilities and exposures (CVEs)
  * A naming system for vulnerabilities
* Common vulnerability scoring system (CVSS)
  * A scoring system for severity
* Common platform enumeration (CPE)
  * A naming system for configuration issues
* Extensible configuration checklist description format (XCCDF)
  * Language for security checklists
* Open vulnerability and assessment language (OVAL)
  * Language for security testing procedures

#### Vulnerability Scans

> The instructor for my bootcamp told us that this is a heavily tested section, and trips up a ton of test takers

* Vulnerability scans
  * Automatically probe systems
* Network discovery scans
  * NMAP - a network scanning tool
  * TCP SYN scanning
    * Single packets sent with the SYN flag set
  * TCP connect scanning
    * Opens a full connection to the remote system
  * TCP ACK scanning
    * Send a packet with ACK set, indicating it's part of an open connection
    * Helps determine firewall rules
  * Xmas scanning
    * FIN, PSH, URG flags are set on packets sent to systems
* Port statuses
  * Open - there is an application that is actively accepting connections
  * Closed - The firewall is allowing access, but there is no application accepting connections
  * Filtered - Unable to determine if a port is open or closed because of a firewall
* Network vulnerability scanning
  * Deeper than a discovery scan
  * Tools contain databases of thousands of known vulnerabilities, and tests that can be performed to identify whether a system is susceptible to each vulnerability
  * False positives and false negatives may occur
  * By default, vulnerability scanners run unauthenticated scans
* TCP ports

|Service|Port|
|-|-|
|FTP|20-21|
|SSH|22|
|Telnet|23|
|SMTP|25|
|DNS|53|
|HTTP|80|
|POP3|110|
|NTP|123|
|Windows file sharing|135, 137-139 (NETBIOS, WINS), 445|
|HTTPS|443|
|LPR/LPD|515|
|Microsoft SQL Server|1433/1434|
|Oracle|1521|
|H.323|1720|
|PPTP|1723|
|RDP|3389|
|HP JetDirect Printing|9100|

* Nessus, Qualys, Rapid7's NeXpose, OpenVAS are all vulnerability scanners
* Aircrack is used to scan wireless networks
* Web vulnerability scanning
  * Structured Query Language (SQL) injection, leveraging poor input validation/sanitization
  * Web vulnerability scanners scour web applications for known vulnerabilities
  * Nessus does this, too, also Acunetix, Nikto, Wapiti, Burp Suite
  * Scan all applications when you begin performing scanning for the first time
  * Scan new applications when moving into production
  * Scan before code changes go to production
  * Scan on a recurring basis
* Vulnerability management workflow
  1. Detection - Identification of a vulnerability
  1. Validation - Confirm the vulnerability is not a false positive
  1. Remediation - Patch, change configurations, implement a workaround
* Penetration testing
  * Actually attempting to exploit systems, not just scan them
  * Done by trained security professionals
  * Process
    1. Planning - agree on scope, rules of engagement
    1. Information gathering and discovery - tools collect information, reconnaissance
    1. Vulnerability scanning - probes for system weaknesses
    1. Exploitation - use automated and manual exploitation tools to defeat system security
    1. Reporting - results of the penetration test, make recommendations
  * Metaspoit is a common tool
  * Types of penetration tests
    1. White box - attackers have detailed information about the target systems
    1. Gray box - attackers have partial knowledge about target systems
    1. Black box - attackers are not provided with any information
    * They should be done in this order

#### Testing Your Software

* Applications often have privileged access
* Apps often handle sensitive information
* They often rely on databases
* Code review
  * AKA peer review
  * Approval of an application's move into production
  * Fagan inspection
    1. Planning
    1. Overview
    1. Preparation
    1. Inspection
    1. Rework
    1. Follow up
* Static testing
  * Done without running it, but rather analyzing source code or compiled app
* Dynamic testing
  * Done in a runtime environment
  * Testers often do not have access to underlying source code
  * Synthetic transactions are scripted transactions with an application with known expected results
* Fuzz testing
  * Different types of input are given to software to test it's limits and find previously undetected flaws
  * Mutation "dumb" fuzzing
    * Takes previous input values and mutates them to create fuzzed input
  * Generational "intelligent" fuzzing
    * Data models used to create new fuzzed input based on understanding of data types used by the system
  * zuff - a tool that performs fuzzing
* Interface testing
  * Different parts of a complex app that must function together are tested
* Misuse case testing
  * Enumerate the known misuse cases
  * How can software be abused?
* Test coverage analysis
  * Estimate the degree of testing conducted
    * Test coverage = number of use cases tested / total number of use cases
  * Branch coverage
    * Has every `if` been executed under all `if` and `else` conditions?
  * Conditional coverage
    * Has every logical test in the code been executed under all sets of inputs?
  * Function coverage
    * Has every function in the code been called and returned results?
  * Loop coverage
    * Has every loop in the code been executed under conditions that cause code execution multiple times, once, and not at all?
  * Statement coverage
    * Has every line of code been executed during the test?
* Website monitoring
  * Passive monitoring
    * Analyze actual network traffic
    * Real user monitoring reassembles the activity of individual users
  * Synthetic monitoring
    * AKA Active monitoring
    * Performing artificial transactions

#### Implementing Security Management Processes

* Log reviews
  * Logging systems should use Network Time Protocol (NTP) to ensure clock synchronization
  * Periodically review logs
* Account management
  * Ensure users only retain authorized permissions and that unauthorized modifications do not occur
  * Example process
    1. Provide a list of users with privileged access
    1. Ask the privilege approval authority to provide a list of authorized users
    1. Compare the two lists
  * Lots of other checks, like terminated users
  * Check paper trails
* Backup verification
* Key performance and risk indicators
  * Monitor key performance and risk indicators
  * Number of open vulnerabilities
  * Time to resolve vulnerabilities
  * Vulnerability/defect recurrence
  * Number of compromised accounts
  * Number of software flaws detected in pre-production scanning
  * Repeat audit findings
  * User attempts to visit known malicious sites
  * Lots more, come up with your own depending on what's important to your org
