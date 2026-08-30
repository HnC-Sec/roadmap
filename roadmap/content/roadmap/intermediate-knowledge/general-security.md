---
date: '2026-08-30T00:00:00Z'
draft: false
title: 'General Security'
weight: 99
topics:
  - The CIA Triad
  - Authorization vs Authentication
  - Threat Modeling
  - Risk and Vulnerability Management
  - Incident Response
  - Auditing
milestones:
  - Understand the tradeoff of various security measures
  - Determine if a control is related to authz or authn
  - Create a threat profile and address each threat
  - Understand common audit frameworks and requirements
knowledge_check:
  - Confidentiality, Integrity, Availability
  - Authz, Authn, RBAC, ABAC, MFA
  - Threat, Threat Profile, Asset, Agent, Control
  - Mitigate, Eliminate, Transfer, Accept, Compensating Control
  - CSIRT, IRP
  - ISO, PCI-DSS, HIPAA, SOX
certifications:
  - CompTIA Security+
  - ISC² CISSP
learning_resources:
  - title: "Professor Messer's SY0-701 Security+ Course"
    cost: "Free"
    time: "~20 Hours"
    url: "https://www.professormesser.com/security-plus/sy0-701/sy0-701-video/sy0-701-comptia-security-plus-course/"
    link_text: "Professor Messer"
    notes: "Complete free video course covering the whole Security+ syllabus. Excellent match for this section."
  - title: "OWASP Threat Modeling"
    cost: "Free"
    time: "2 Hours"
    url: "https://owasp.org/www-community/Threat_Modeling"
    link_text: "OWASP"
    notes: "Practical starting point for threat modeling, including STRIDE and the four-question framework."
  - title: "Threat Modeling Manifesto"
    cost: "Free"
    time: "20 Minutes"
    url: "https://www.threatmodelingmanifesto.org"
    link_text: "Threat Modeling Manifesto"
    notes: "Short statement of values and principles from practitioners in the field. Good orientation before picking a method."
  - title: "NIST SP 800-30 - Guide for Conducting Risk Assessments"
    cost: "Free"
    time: "4 Hours"
    url: "https://csrc.nist.gov/pubs/sp/800/30/r1/final"
    link_text: "NIST"
    notes: "The reference document for how risk assessment is actually done. Dense, but authoritative."
  - title: "NIST SP 800-61 - Computer Security Incident Handling Guide"
    cost: "Free"
    time: "4 Hours"
    url: "https://csrc.nist.gov/pubs/sp/800/61/r2/final"
    link_text: "NIST"
    notes: "The standard incident response lifecycle that most organizations base their plans on."
  - title: "MITRE ATT&CK"
    cost: "Free"
    time: "Varies"
    url: "https://attack.mitre.org"
    link_text: "MITRE"
    notes: "Catalogue of real-world attacker tactics and techniques. Invaluable for building realistic threat profiles."
  - title: "CIS Critical Security Controls"
    cost: "Free (registration)"
    time: "3 Hours"
    url: "https://www.cisecurity.org/controls"
    link_text: "CIS"
    notes: "A prioritized, practical list of controls. The best answer to 'what should we actually do first?'"
  - title: "Threat Modeling: Designing for Security"
    cost: "~$45"
    time: "~15 Hours"
    url: "https://shostack.org/books/threat-modeling-book"
    link_text: "Adam Shostack"
    notes: "The standard book on the subject, by the author of STRIDE's practical form."
  - title: "Jason Dion - CompTIA Security+ (SY0-701)"
    cost: "~$20"
    time: "~25 Hours"
    url: "https://www.udemy.com/course/comptia-security-sy0-701-complete-course-practice-exam/"
    link_text: "Udemy"
    notes: "Paid Security+ course with practice exams, frequently discounted."
---

Everything up to this point has been about how technology works. This section is about the ideas that turn that knowledge into security work: what you are actually protecting, who might want to take it, how you decide what to do about that, and what happens when something goes wrong anyway.

These concepts sound abstract, and they are the part that beginners most often skip in favour of tools. That is a mistake. Tools change constantly; this framework is what tells you which tools to reach for and why. It is also the language that security teams, auditors, and management all speak, so being fluent in it is what lets you be taken seriously.

## The CIA Triad

The **CIA triad** is the classic model of what security is protecting. It has nothing to do with the intelligence agency.

- **Confidentiality** — only the people who should see the information can see it. Broken by data breaches, eavesdropping, and over-broad permissions. Protected by encryption and access control.
- **Integrity** — the information is correct and has not been altered without authorization. Broken by tampering, corruption, and unauthorized changes. Protected by hashing, digital signatures, and change control. Integrity failures are often more damaging than confidentiality failures, because you may not know which data you can still trust.
- **Availability** — the information and systems are there when needed. Broken by denial-of-service attacks, ransomware, and hardware failure. Protected by redundancy, backups, and capacity planning.

The value of the triad is that it forces you to ask which of the three you actually care about, and to notice that they pull against each other. Encrypting everything strengthens confidentiality and can weaken availability, because a lost key means lost data. Aggressive backups strengthen availability and can weaken confidentiality, because now the data exists in more places. Locking a system down tightly protects it and makes it harder to use — and a control users find unbearable is a control they will find a way around.

This is the central skill of security work: it is not about maximizing protection, it is about making deliberate trade-offs and being able to explain them. Some fields add related properties such as **authenticity** and **non-repudiation** (proof that a specific party performed an action and cannot credibly deny it), but the three above remain the foundation.

## Authentication and Authorization

These two words look alike, get abbreviated confusingly, and are constantly mixed up.

**Authentication (authn)** answers *who are you?* It is the process of proving identity. **Authorization (authz)** answers *what are you allowed to do?* It is the process of deciding whether an already-identified party may perform an action.

Authentication comes first, but the two fail differently and are attacked differently. A password guess is an authentication attack; accessing another user's records by changing an ID in a URL is an authorization attack. Broken authorization is one of the most common serious flaws in real applications, precisely because developers test that login works and forget to test that a logged-in user cannot reach someone else's data.

Authentication traditionally relies on **factors** — categories of evidence:

- Something you **know** (a password, a PIN)
- Something you **have** (a phone, a hardware token, a smart card)
- Something you **are** (a fingerprint, a face)

**MFA (Multi-Factor Authentication)** requires evidence from more than one category. Two passwords are not MFA; a password plus a hardware key is. MFA is effective because stealing a password no longer grants access on its own — though not all second factors are equal, and SMS codes are notably weaker than hardware security keys or app-based codes because phone numbers can be hijacked.

Authorization is usually organized with a model:

- **RBAC (Role-Based Access Control)** assigns permissions to roles and roles to users. Simple, widely used, and easy to audit. It struggles when permissions need to depend on context.
- **ABAC (Attribute-Based Access Control)** decides based on attributes of the user, the resource, the action, and the environment — for example, "a manager may view a payroll record for their own department during business hours". Far more flexible, and far harder to reason about and review.

Two principles apply regardless of model. **Least privilege** means giving each account only the access it needs to do its job, and nothing more. **Separation of duties** means splitting sensitive operations so that no single person can complete one alone. Both exist to limit the damage a compromised or dishonest account can do.

## Threat Modeling

**Threat modeling** is the practice of working out, deliberately and in advance, what could go wrong with a system — before an attacker does it for you.

The vocabulary matters here because it is used precisely:

- An **asset** is something worth protecting: data, a system, a service, a reputation.
- A **threat** is a potential event that would harm an asset.
- A **threat agent** (or actor) is who or what could cause it — an organized criminal group, a competitor, a careless employee, a flood.
- A **vulnerability** is a weakness that could let a threat happen.
- A **control** is a measure that reduces the chance or the impact.
- A **threat profile** is the resulting picture of which threats matter for *your* system and *your* likely adversaries.

That last point is the whole reason to do this. A hobby blog and a hospital do not face the same adversaries and should not spend the same effort. Defending against a bored scanner is a different job from defending against a well-funded group that specifically wants your data.

A widely used way in is Adam Shostack's four questions:

1. **What are we working on?** Draw the system. A data flow diagram showing components, data stores, and trust boundaries is usually enough. Most of the value comes from this step alone, because teams routinely discover they disagree about how their own system works.
2. **What can go wrong?** Enumerate threats. **STRIDE** is a helpful checklist here — Spoofing, Tampering, Repudiation, Information disclosure, Denial of service, and Elevation of privilege — applied to each element of the diagram. MITRE ATT&CK is useful for grounding this in techniques attackers genuinely use.
3. **What are we going to do about it?** Decide on a response for each threat (see risk management below).
4. **Did we do a good job?** Review it. A threat model is a living document, not a one-time deliverable.

Threat modeling is cheapest and most valuable early in a design, when changing an architecture is still a conversation rather than a rewrite.

## Risk and Vulnerability Management

**Risk** is the combination of how likely something is and how bad it would be. That combination is what lets you compare unlike problems and decide what to fix first, because you will never have the resources to fix everything.

For any identified risk there are a small number of legitimate responses:

- **Eliminate (avoid)** — remove the risk entirely by not doing the risky thing: decommission the service, stop collecting the data. The strongest option and often the most overlooked. Data you do not hold cannot be stolen.
- **Mitigate (reduce)** — apply controls to lower the likelihood or the impact. This is most security work.
- **Transfer** — shift the financial consequence to someone else, typically through insurance or a contract. Note that you can transfer cost, but not responsibility or reputational damage.
- **Accept** — decide the risk is tolerable and do nothing. This is a legitimate choice when it is made knowingly, documented, and signed off by someone with the authority to own the consequences. Undocumented acceptance is just ignorance.

A **compensating control** is an alternative measure used when the preferred control is not possible. If a legacy system cannot support MFA, you might compensate by isolating it on its own network segment, restricting access to specific workstations, and monitoring its logs closely. Compensating controls are a normal part of real environments and a constant topic in audits.

**Vulnerability management** is the ongoing operational process built on all this: discover what you have (you cannot protect an asset you do not know about), scan for known weaknesses, prioritize them, remediate, and verify. Prioritization is where judgement lives. A **CVE (Common Vulnerabilities and Exposures)** identifier names a specific known vulnerability, and **CVSS (Common Vulnerability Scoring System)** gives it a severity score from 0 to 10 — but CVSS describes the flaw in the abstract, not your situation. A critical vulnerability in a service that is not exposed and not running matters less than a medium one on your internet-facing login page. Whether an exploit exists in the wild often matters more than the score.

## Incident Response

Prevention fails eventually. **Incident response (IR)** is the discipline of handling that competently instead of chaotically.

An **IRP (Incident Response Plan)** is the written document saying what happens when something goes wrong: who is called, who can make which decisions, how people communicate if normal systems are untrusted, when law enforcement or regulators get involved, and what the legal reporting obligations are. It is written in advance precisely because nobody makes good decisions at 3am during a crisis.

A **CSIRT (Computer Security Incident Response Team)** is the group that carries the plan out. In a large organization it is dedicated staff; in a small one it is a named handful of people with other jobs. What matters is that the roles are decided beforehand.

The commonly used lifecycle, from NIST SP 800-61, has four phases:

1. **Preparation** — plans, tooling, logging, training, and exercises. By far the highest-leverage phase, and the one most often skipped. If you are not collecting logs before the incident, you will not have them during it.
2. **Detection and Analysis** — noticing that something happened and working out what. Determining scope is the hard part: which systems, which accounts, what data, and since when.
3. **Containment, Eradication, and Recovery** — stop the spread, remove the attacker's access and tooling, restore normal service, and confirm they are actually gone. Containment involves a real tension: pulling a machine off the network stops the damage but may destroy evidence and warn the attacker.
4. **Post-Incident Activity** — the lessons-learned review. Feed the findings back into preparation. This is where an incident becomes an improvement instead of just a bad week.

Two cultural points are worth internalizing early. Reviews should be **blameless** — if people fear punishment they will hide information, and hidden information is how a small incident becomes a large one. And **evidence handling matters**: notes, timelines, and preserved images may end up in a legal process, so record what you did and when as you go.

## Auditing

**Auditing** is the process of checking, and being able to demonstrate, that controls exist and work. Some of it is internal and voluntary; a lot of it is driven by outside requirements.

The frameworks and regulations you will hear named most often:

- **ISO/IEC 27001** — an international standard for an information security management system. Certification says an organization has a documented, reviewed process for managing security, not that any particular technical control is in place.
- **PCI-DSS (Payment Card Industry Data Security Standard)** — mandatory for anyone handling payment card data. Unusually prescriptive: it names specific technical requirements rather than general principles.
- **HIPAA** — US law governing the privacy and security of health information.
- **SOX (Sarbanes-Oxley)** — US law on financial reporting for public companies. Its security relevance is in the controls around the integrity of financial systems and data.
- **SOC 2** — a report on a service organization's controls, very commonly requested by business customers.
- **GDPR** — EU regulation on personal data, with real reach beyond Europe and significant penalties.

Compliance and security are related but not the same. **Compliance is a floor, not a ceiling.** An organization can pass every audit and still be badly insecure, because a framework can only ever require what is general enough to apply to everyone. It is equally possible to be genuinely secure and fail an audit for want of documentation. Treating a compliance certificate as proof of security is one of the most common and most expensive mistakes in the industry.

That said, do not dismiss it. Compliance requirements are frequently the reason security work gets funded at all, and the discipline they impose — inventories, documented processes, evidence that a control actually runs — is real security value even when the motivation is a checkbox. Learning to work with auditors rather than against them is a genuinely useful professional skill.
