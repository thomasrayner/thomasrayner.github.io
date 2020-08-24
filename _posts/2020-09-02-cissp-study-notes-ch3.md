---
layout: post
title: CISSP Study Notes Chapter 3 - Business Continuity Planning
date: 2020-09-02 07:30
author: thmsrynr
comments: true
categories: [cissp, security, certifications]
---
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

* [Chapter 1: Security Governance Through Principles and Policies](.\2020-08-19-cissp-study-notes-ch1.md)
* [Chapter 2: Personnel Security and Risk Management Concepts](.\2020-08-26-cissp-study-notes-ch2.md)

## Chapter 3: Business Continuity Planning

### What this chapter is about

This chapter discusses how to identify, analyze, and prioritize business continuity requirements, including developing the scope and the plan. It also talks about business impact analysis, and how to participate in BC planning and exercises.

### My key takeaways and crucial points

#### Planning for Business Continuity (BC)

* *Business Continuity Planning* - BCP. The goal is to implement policies, procedures and processes so that a disruptive event has as little impact on the business as possible.
* BC activities are focused at a high level and center on business processes (strategic)
* DR (disaster recovery) focuses on technical activities (tactical)
* Overall BCP goal is providing a quick, calm, efficient response to emergencies, enhance ability to recover from a disruption

#### Business Organization Analysis

* Operational departments - responsible for core services
* Critical support services - other groups responsible for systems upkeep
* Corporate security teams - first responders
* Senior executives - ongoing viability of the organization
* Be sure to account for headquarters and also branch offices

#### BCP Team Selection

* Representatives from each org's departments
* Team members from the functional areas
* IT subject matter experts
* Cybersecurity
* Facility management
* Attorneys
* Human resources
* Public relations
* Senior management
  * Without an active senior management presence, your BCP plan will suffer or fail

#### Resource Requirements

* Four elements
  * Project scope and planning
  * Business impact assessment
  * Continuity planning
  * Approval and implementation
* BCP is often expensive, requires a large amount of resources
  * Being out of operation is more expensive - identify the costs incurred by the business for each day that the business is down

#### Legal and Regulatory Requirements

* Public firms have a fiduciary responsibility to have these plans, also financial intuitions, pharma manufacturers
* Service level agreements likely obligate a BCP

#### Business Impact Assessment (BIA)

* Identifies resources that are critical to an organization's ongoing viability and threats posed to those resources
* *Quantitative decision making* - Use of numbers
* *Qualitative decision making* - Non-numerical factors

#### Identify Priorities

* Gather input from **all** parts of the org
  * Everybody has different priorities
  * What IT/security/management thinks is mission critical may not be what the sales/finance people think is critical
* Quantitative metrics
  * *Asset value* - AV. Monetary value of each asset
  * *Maximum tolerable downtime* - MTD. Max length of time a business function can be inoperable before it harms the business.
  * *Maximum tolerable outage* - MTO. Same metric as MTD.

#### Risk Identification

* Natural risks vs man-made risks
* The below are all considered **natural threats** but might trip you up
  * Prolonged power outages
  * Building collapses
  * Transportation failures
  * Internet disruptions
  * Service provider outages

#### Likelihood Assessment

* *Annualized rate of occurrence* - ARO. A percentage that represents how many times in one year an event is likely to occur.
  * 0.5 = once every two years
  * 12 = once every month

#### Impact Assessment

* *Exposure factor* - EF. Amount of damage a risk poses to the asset. Percentage of the asset's value.
  * If a fire reduces the value of a business by 70%, the EF is 70.
* *Single loss expectancy* - SLE. Monetary loss that is expected each time the risk materializes.
  * SLE = AV x EF
* *Annualized loss expectancy* - ALE. Monetary loss that the business expects to result of a risk harming the asset over the course of a year.
  * ALE = SLE x ARO
  * Allows you to budget annually for countermeasures for threats that may occur on a non-annual basis.

#### Resource Prioritization

* Create a list of all risks
* Sort by descending order according to ALE

#### Continuity Planning - Strategy Development

* Depends on the prioritized list of concerns according to ALE
  * Determines what risks are most important to the business
* Refer to MTD estimates

#### People

* **PEOPLE ARE ALWAYS FIRST**
  * Ensuring that the people in your organization before, during, and after an emergency is **always** the first priority
  * People are your most valuable asset
  * Any time human safety is a possible answer to a question, you must remember that **human safety is always the most important**

#### Buildings and Facilities

* *Hardening provisions* - Protects existing facilities against risks defined in strategy development phase
* *Alternate sites* - If you can't harden a facility, BCP should identify an alterative site where business activities can resume asap

#### Infrastructure

* *Physical hardening systems* - Protective measures
* *Alternative systems* - Redundancy

#### Plan Approval and Implementation

* Senior management approval and buy-in is essential to the success of the overall BCP effort

#### Plan Implementation

* BCP team should supervise the conduct of an appropriate BCP maintenance program and ensure that the plan remains responsive to evolving risk

#### Training and Education

* Personnel who are involved in the plan need training
  * On the overall plan
  * On their specific responsibilities
* Everyone in the org
  * Plan overview
* People with direct BCP responsibilities
  * Trained and evaluated on their tasks
  * At least one backup person needs training for each task

#### BCP Documentation

* Written continuity document
* Historical record of the BCP process for future personnel to understand the current process
* Documents reviewed by people outside the BCP team for a "sanity check"

#### Continuity Planning Goals

* The plan should describe the goals of the continuity planning
* Ensure continuous operation of the business in the face of an emergency
* Meeting SLAs and KPIs
* Continuity plan elements
  * Statement of Importance
    * Reflects how critical the BCP is
  * Statement of Priorities
    * Identify priorities phase of business impact assessment
    * List functions that are critical to continued business operations in a prioritized order
  * Statement of Organizational Responsibility
    * Basically echoes the sentiment that "business continuity is everybody's responsibility"
  * Statement of Urgency and Timing
    * Outlines the implementation timetable
  * Risk Assessment
    * Recaps the decision making process from BIA
    * For quantitative analysis, the AV, EF, ARO, SLE, and ALE figures should be included
    * For qualitative analysis, the thought process behind the risk analysis should be included
  * Risk Acceptance/Mitigation
    * Risks that are deemed acceptable - list the reasons
    * Risks that are deemed unacceptable - list provisions and processes in place to reduce the risk
    * Resist the statement "we accept this risk" and force the documentation of risk acceptance decisions
      * Force accountability for risk planning/acceptance
      * Protect yourself from auditor scrutiny
  * Vital Records Program
    * States where critical records will be stored
    * How to make backups and store them
  * Emergency Response Guidelines
    * Organization and individual responsibilities for emergency response
    * Immediate response procedures for security, safety, fire suppression, notification of emergency response agencies
    * A list of individuals who should be notified of incident
    * Secondary response procedures for first responders to follow while waiting for BCP team to assemble
    * Should be **easily** accessible

#### Maintenance

* BCP should not be disbanded, should continue to meet periodically
* Practice good version control
* Include BCP responsibilities in job descriptions, include in performance review process
