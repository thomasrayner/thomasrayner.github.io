---
layout: post
title: CISSP Study Notes Chapter 2 - Personnel Security and Risk Management Concepts
date: 2020-08-26 07:30
author: thmsrynr
comments: true
categories: [cissp, security, certifications]
---
This chapter is about working with risk. Human weaknesses are discussed at the beginning and end of the chapter in the form of job descriptions, and then about training. This chapter also discusses how to think about risk, define risks correctly, and how to think about countermeasures and other responses to risk.

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

## Chapter 2: Personnel Security and Risk Management Concepts

### My key takeaways and crucial points

#### Personnel Security Policies and Procedures

* Humans are the weakest element in any security solution.
* Making a *job description* involves setting a classification for the job, screening candidates, hiring and training.
* Job descriptions are important to a security solution.
  * What kind of security access is needed to perform job responsibilities?
* *Separation of duties* - Critical, significant, and sensitive work tasks are divided among several individuals, preventing one person from having any ability to undermine or subvert security mechanisms.
* *Principle of least privilege* - Giving people the least amount of access and privileges that still allows them to perform their duties.
  * Protects against *collusion* - when two or more people work together to undermine security for the purposes of fraud, theft, or espionage.
* *Job responsibilities* - Specific work tasks.
* *Job rotation* - Rotating employees among multiple job positions. Provides knowledge redundancy, and reduces risk of fraud, theft, misuse, etc.
  * If misuse occurs, someone else performing the job will detect it. Additionally, misuse becomes more likely as people become increasingly familiar with their work tasks and how their privileges may be abused.
* *Cross-training* - Workers are prepared to perform other job positions, but they are not rotated.
* Job descriptions are not just for the hiring process, but need to be maintained throughout the life of the organization.
* *Onboarding* - The process of adding new employees.
* *Offboarding* - The reverse of onboarding.
* Terminations should take place with at least one witness. People who are terminating should be escorted off the premises. Organization-specific identification and access must all be revoked and collected.
* *Exit interview* - A meeting that takes place with an offboarding employee.
  * Make sure all organization equipment and supplies are returned
  * Remove or disable user accounts
  * Human resources remuneration gets handled (pay unused vacation time, etc.)
  * Arrange for security department to accompany employee while they gather personal belongings
  * Inform security personnel the ensure ex-employee doesn't attempt to reenter the building without an escort
  * Remind the employee of liabilities and restrictions based on employment agreement, nondisclosure agreement, etc.

#### Vendor, Consultant, and Contractor Agreements and Controls

* Vendor controls are used to define levels of performance and expectations for organizations and people external to the primary organization.
* *Service level agreement* - SLA. The document that often defines these expectations. For instance:
  * System uptime
  * Maximum consecutive downtime
  * Peek load
  * Responsibility for diagnostics
  * Failover time
* SLAs commonly contain financial and other remedies for violations. Should include a focus on protecting and improving security.

#### Privacy Policy Requirements

* Some definitions for *privacy*
  * Active prevention of unauthorized access to information
  * Freedom from unauthorized access
  * Freedom from being observed
* *Personally identifying information* - PII. Any data that can be easily and/or obviously traced back to the person of origin or concern.
  * Examples: Phone number, email address, social security number.
  * NOT PII: MAC address, operating system type, high school mascot.
  * Student ID numbers are **not** PII. They can exist at different institution.
* Privacy legislation:
  * *HIPAA* - Health Insurance Portability and Accountability Act
  * *SOX* - Sarbanes-Oxley Act of 2002
  * *FERPA* - Family Educational Rights and Privacy Act
  * *Gramm-Leach-Bliley Act*
  * *GDPR* - General Data Protection Regulation
  * *PCI DSS* - Payment Card Industry Data Security Standard

#### Security Governance

* *Security governance* - Supporting, defining, directing security efforts.
  * Third-party governance may be mandated by law, regulation, standards, etc.
* *Documentation review* - Performed before any on-site inspection takes place.
* *ATO* - Authorization to Operate - related to military and government contracts.

#### Understand and Apply Risk Management Concepts

* *Risk* - The possibility that something to happen to damage, destroy, or disclose data or other resources.
* *Risk management* - Process of identifying factors of risk and evaluating them in light of data value and countermeasure cost, and implementing cost-effective solutions for mitigating or reducing risk.
  * Supports the mission of the organization.
  * Reduce risk to an **acceptable level**.
* *Asset* - Anything that should be protected. Something important enough to protect.
* *Asset valuation* - A dollar value assigned to an asset.
* *Threats* - Any potential occurrence that may cause an unwanted outcome for a specific asset.
* *Vulnerability* - A weakness in an asset or the absence of a safeguard.
* *Exposure* - Being susceptible to asset loss due to a threat.
* *Risk* - The possibility that a threat will exploit a vulnerability and cause harm to an asset.
  * **Risk = Threat * Vulnerability**
* *Safeguards* - A security control, countermeasure, or anything else that removes or reduces a vulnerability or protects against one or more threats.
* *Attack* - The exploitation of a vulnerability by a threat agent.
* *Breach* - When a security mechanism is bypassed or thwarted.

#### Risk Assessment/Analysis

* Primarily an exercise for upper management.
* No way to eliminate 100% of risks. Only reduce them to an acceptable level.
* *Quantitative* risk analysis assigns real dollar figures to the loss of an asset.
  * Ex: You'd lose $15,000 if a car was stolen from your fleet.
  * Steps:
    1. Assign an asset value (AV) - inventory assets
    1. Calculate the exposure factor (EF - the percentage of loss experienced if a risk is realized) and single loss expectancy (SLE - the cost associated with a single realized risk against an asset)
    1. Probability that threat will occur within 1 year (ARO - annualized rate of occurrence. Once every two years is 0.5. Every month is 12.) - threat analysis
    1. Find the annualized loss expectancy (ALE - possibly yearly cost of all instances of a realized threat), calculate changes to ARO and ALE based on applied countermeasures. **ALE = SLE * ARO**. How much it would cost if this happened, times how likely that thing will happen within one year, equals your ALE.
    1. Perform a cost/benefit analysis for each countermeasure. ALE before safeguard minus the ALE after implementing the safeguard, minus the annual cost of the safeguard equals the value of that safeguard. If the value is negative, it's not worth it.

> Fun Fact! I did a session on how to get everything you've ever wanted from your stakeholders called ["How to Take Risks Without Getting Clawed in the Face"](https://www.youtube.com/watch?v=iEReCcjNqQo&list=PLZFOfztme55Eg90hA6vaSGZUaf0s9skGK&index=2) that covers using a quantitative risk analysis approach to win every "I want something" conversation you'll ever have.

* *Qualitative* risk analysis assigns subjective and intangible values to the loss of an asset.
  * Ex: You'd lose the trust of your customers if you customer contact information was exposed.
  * Scenario-based. Scenarios are a written description of a single major threat.
  * *Delphi technique* - Anonymous feedback-and-response processed used to enable a group to reach an anonymous consensus. Elicits honest and uninfluenced responses.
  * May also perform brainstorming, focus groups, surveys, etc.

#### Risk Responses

* *Risk mitigation* - Implementation of safeguards to eliminate or block threats.
* *Risk assignment* - Transferring risk so that the cost of a loss falls onto another entity or organization. Such as purchasing insurance or outsourcing.
* *Risk acceptance* - Cost/benefit analysis shows that countermeasure costs outweigh the possible cost of loss from a risk, so you may just decide that you'll do nothing about the risk other than acknowledge it and periodically revisit your decision.
* *Risk deterrence* - Implementing deterrents like auditing, security cameras, warning banners.
* *Risk avoidance* - Selecting an alternate option that has less risk.
* *Risk rejection* - Unacceptable but possible, ignore the risk, deny it exists, hope it is never realized.
* *Residual risk* - Comprises threats to specific assets against which one chooses not to implement a safeguard. Risk that is accepted.
* *Total risk* - Risk faced if no safeguards were implemented.
  * Threats x Vulnerabilities x Asset value = Total risk

#### Countermeasure Selection and Implementation

* Cost of countermeasure should be...
  * less than cost of asset
  * less than benefit of countermeasure
* Result should make cost of an attack greater than derived benefits
* Countermeasure should provide a solution to a REAL problem. Not just sound cool.
* Benefit of countermeasure should  not depend on its secrecy. That's security through obscurity.
* Countermeasures should...
  * Be testable and verifiable
  * Provide consistent and uniform protection
  * Have few or no dependencies
  * Require minimal human intervention after deployment
  * Be tamperproof
  * Have overrides for privileged operators only
  * Provide fail-safe and/or fail-secure options

#### Types of Controls

* *Technical* - hardware or software
* *Administrative* - policies and procedures
* *Physical* - items you can physically touch
* Security controls:
  * *Deterrent* - Discourage violation of security policies
  * *Preventative* - Thwart or stop unwanted activity
  * *Detective* - Discover or detect unwanted activity
  * *Compensating* - Provide options to other existing controls
  * *Corrective* - Modifies the environment to return systems to normal after unwanted activity
  * *Recovery* - Extension of corrective, but more advanced.
  * *Directive* - Direct, confine, or control actions of subjects to enforce or encourage compliance.
* *Security control assessment* - SCA. Formal evaluation of security infrastructure's individual mechanisms against a baseline or expectation. See NIST 800-53A.

#### Continuous Improvement

* Risk analysis is performed to provide management with details needed to decide how to respond to risk.
* Risk analysis/assessment is always "point in time" and must be periodically revisited.

#### Risk Frameworks

* See NIST 800-37 for Risk Management Framework (RMF) which has these steps:
  * *Categorize* information
  * *Select* initial set of baseline controls
  * *Implement* controls
  * *Assess* the controls
  * *Authorize* information system operation based on determination of the risk
  * *Monitor* controls in an ongoing basis

#### Establish and Maintain a Security Awareness, Education, and Training Program

* *Awareness* - prerequisite to security training. Make security a recognized entity for users.
* *Training* - teaching employees to perform their work tasks and to comply with security policy.
* *Education* - more detailed training where users learn much more than they actually need to know to perform their work tasks.

#### Manage the Security Function

* Measurable security means that there is a clear benefit provided, and one or metrics are recorded and analyzed.
