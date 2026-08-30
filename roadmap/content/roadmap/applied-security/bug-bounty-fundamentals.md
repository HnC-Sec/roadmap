---
title: "Bug Bounty Hunting"
weight: 40
topics:
  - Understanding Bug Bounty Programmes
  - Recon for Bug Bounty
  - Vulnerability Hunting
  - Triage and Reporting
milestones:
  - Read the programme policy, scope, and disclosure terms of at least 5 bug bounty programmes before testing anything
  - Submit your first valid (non-duplicate, in-scope) bug bounty report
  - "Build a personal recon automation pipeline using `subfinder` + `httpx` + `nuclei`"
  - Find and report an IDOR or access control vulnerability on a real programme
  - Write a report that successfully upgrades a finding's severity through impact demonstration
  - Participate in a private programme invitation (typically unlocked by consistent valid reports)
  - Achieve at least one Hall of Fame acknowledgement or cash payout (proof of concept for real-world skill)
knowledge_check:
  - The difference between a **VDP** and a **bug bounty programme** — and why you should care about the difference before you report
  - What **safe harbour** means in a programme policy and why you should verify it exists before testing
  - Why **scope discipline** is critical — what the consequences of out-of-scope testing can be legally and reputationally
  - What a **duplicate** is and why high-frequency bug classes on popular targets get duplicated quickly
  - How to demonstrate **impact** in a report to justify a severity rating — what triagers look for
  - What a **business logic vulnerability** is and why automated scanners typically miss them
  - How **subdomain takeover** works and why it is a common finding in large programmes
  - The role of **CVSS** in severity decisions and why triagers sometimes disagree with researcher scores
  - What **P1/P2/P3/P4** severity tiers mean on major platforms like HackerOne and Bugcrowd
  - Why **chaining** low-severity findings can result in higher payouts and how to demonstrate the chain
certifications:
  - "**BSCP** (Burp Suite Certified Practitioner) — demonstrates advanced web exploitation skill"
  - "**eWPT / eWPTX** (eLearnSecurity Web Penetration Tester) — practical, web-focused"
  - Hall of Fame acknowledgements on HackerOne, Bugcrowd, Intigriti, or company-direct programmes carry real weight
learning_resources:
  - title: "HackerOne"
    cost: "Free"
    time: "Varies"
    url: "https://www.hackerone.com"
    link_text: "HackerOne"
    notes: "Largest managed bug bounty platform, good for beginners"
  - title: "Intigriti"
    cost: "Free"
    time: "Varies"
    url: "https://www.intigriti.com"
    link_text: "Intigriti"
    notes: "European-focused platform, strong researcher community"
  - title: "Bugcrowd"
    cost: "Free"
    time: "Varies"
    url: "https://www.bugcrowd.com"
    link_text: "Bugcrowd"
    notes: "Well-established platform with diverse programme types"
  - title: "YesWeHack"
    cost: "Free"
    time: "Varies"
    url: "https://www.yeswehack.com"
    link_text: "YesWeHack"
    notes: "European platform, growing rapidly"
  - title: "ProjectDiscovery"
    cost: "Free"
    time: "Varies"
    url: "https://projectdiscovery.io"
    link_text: "ProjectDiscovery"
    notes: "Open-source recon tooling ecosystem (`nuclei`, `subfinder`, `httpx`, `notify`)"
  - title: "NahamSec on YouTube"
    cost: "Free"
    time: "Varies"
    url: "https://www.youtube.com/c/NahamSec"
    link_text: "YouTube"
    notes: "Practical bug bounty methodology and live streams"
  - title: "HackerOne Hacktivity"
    cost: "Free"
    time: "Varies"
    url: "https://hackerone.com/hacktivity"
    link_text: "HackerOne"
    notes: "Disclosed reports from public programmes — the best way to learn what real vulnerabilities look like"
  - title: "Pentester Land"
    cost: "Free"
    time: "Varies"
    url: "https://pentester.land/list-of-bug-bounty-writeups.html"
    link_text: "Pentester Land"
    notes: "Curated writeup aggregator"
  - title: "Bug Bounty Bootcamp"
    cost: "Paid"
    time: "Varies"
    url: "https://nostarch.com/bug-bounty-bootcamp"
    link_text: "No Starch Press"
    notes: "By Vickie Li — a structured, book-length introduction to finding and reporting bugs"
---

## Bug Bounty Hunting

Bug bounty programmes allow security researchers to legally test the security of real-world systems and receive compensation for valid, in-scope vulnerability reports. This is the applied, real-world extension of the skills built in the Web Application Security and Penetration Testing sections — but with important differences in methodology, scope discipline, and communication.

> **Prerequisite Check:** Bug bounty hunting requires solid web application security skills, a working knowledge of network and application enumeration, and the ability to write clear vulnerability reports. Jumping into bug bounties without these foundations leads to frustration, duplicate reports, and out-of-scope activity. Complete the Web Application Security section first.

---

### General Topics

**Understanding Bug Bounty Programmes**
- Public vs. private programmes — how to get invitations to private programmes
- Managed platforms: HackerOne, Bugcrowd, Intigriti, YesWeHack, Synack
- Disclosure policies: coordinated disclosure, full disclosure, responsible disclosure
- VDP (Vulnerability Disclosure Programme) vs. bug bounty — key differences
- Reading and understanding a programme's **scope** and **out-of-scope** rules
- Safe harbour clauses and legal protections for researchers
- Understanding severity ratings: Critical, High, Medium, Low, Informational

**Recon for Bug Bounty**
- Subdomain enumeration at scale: `subfinder`, `amass`, `assetfinder`, `dnsx`, `httpx`
- Discovering forgotten or shadow IT assets: old subdomains, staging environments, admin panels
- JavaScript endpoint extraction: `LinkFinder`, `SecretFinder`, `JSScanner`
- Parameter discovery: `arjun`, `paramspider`, `waybackurls`
- Cloud asset enumeration: S3 bucket misconfigurations, exposed cloud functions
- Continuous monitoring: setting up alerts for new assets (e.g. `notify`, `chaos` by ProjectDiscovery)
- Using Shodan and Censys to find exposed services belonging to a target

**Vulnerability Hunting**
- Prioritising targets: large scope programmes vs. narrow scope — where to focus
- Bug classes most common in real-world programmes: IDOR, SSRF, XSS, SQLi, auth bypasses, business logic flaws
- Business logic vulnerabilities: rate limiting bypasses, price manipulation, workflow bypasses
- Chaining low-severity findings into a high-impact report
- Avoiding common traps: self-XSS, issues requiring physical access, DoS without impact proof

**Triage and Reporting**
- What makes a good bug bounty report: clear title, affected URL, steps to reproduce, impact, PoC
- CVSS scoring in a bug bounty context
- Communicating professionally with triage teams — patience and clarity
- Handling duplicates and informational verdicts constructively
- Disputing a severity rating respectfully

