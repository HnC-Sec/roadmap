---
title: "CTF and Lab Practice"
weight: 10
---

## CTF and Lab Practice

At some point you have to stop reading and start breaking things. CTF competitions and lab environments are where that happens. You will encounter real vulnerability classes, make a lot of mistakes, and slowly develop a sense for how to approach something you have never seen before.

This section is intentionally first in the Applied Security track because it gives you a low-stakes place to build practical skills before you touch real systems or real programmes.

> **Before you start:** You should be comfortable in a Linux terminal, or Window's command prompt and understand basic networking (ports, protocols, how HTTP works), and have at least some scripting ability. If those feel shaky, work through the Basics sections first.

---

### What are CTFs?

Capture the Flag competitions are security challenges where you find and exploit vulnerabilities to retrieve a "flag" — usually a string in the format `CTF{something}` that proves you solved the challenge. There are several formats:

- **Jeopardy style** — categories of standalone challenges (Web, Crypto, Pwn, Forensics, Reverse Engineering, OSINT, Misc). Most beginner events use this format.
- **Attack/Defence** — teams run identical vulnerable services and attack each other while patching their own. More advanced.
- **King of the Hill** — teams compete to own and hold a single target machine.

HackTheBox and TryHackMe are not CTFs in the traditional sense but serve a similar purpose: intentionally vulnerable machines and labs that teach real techniques in a legal, contained environment.

---

### General Topics

**Getting your environment set up**
- Installing Kali Linux or Parrot OS (as a VM is fine to start — VirtualBox or VMware with host-only or NAT networking)
- Understanding why you use a separate attack VM rather than your daily machine
- Basic Kali navigation: where tools live, how to update, keeping things tidy

**Core tooling you will use constantly**
- `nmap` for port scanning and service enumeration
- `netcat` for connecting to services, testing, and basic shell handling
- `gobuster` or `ffuf` for directory and vhost fuzzing
- `john` and `hashcat` for password cracking
- `Wireshark` for reading packet captures
- CyberChef for encoding, decoding, and data transformation puzzles

**How to approach a challenge**
- Enumerate before you exploit — you cannot attack what you have not found
- Taking notes as you work (not after) and why it matters
- Using writeups ethically: only after a box retires or a CTF ends
- Building a personal writeup archive from the start (GitHub, Obsidian, a text file — whatever sticks)

**Privilege escalation basics**
- What "user flag" vs. "root flag" means in lab context
- Common Linux privesc vectors: SUID binaries, sudo misconfigurations, writable cron jobs, weak file permissions
- Common Windows privesc vectors: SeImpersonatePrivilege, unquoted service paths, AlwaysInstallElevated
- Automated enumeration tools: `LinPEAS`, `WinPEAS` — what they tell you and what they miss

**OSINT basics** (comes up in CTFs and carries into real work)
- `whois`, `dig`, `nslookup`
- Google Dorking (`site:`, `filetype:`, `inurl:`)
- `theHarvester` for email and subdomain gathering

---

### Milestones

- [ ] Set up a dedicated lab VM running Kali or Parrot OS
- [ ] Complete the TryHackMe "Pre-Security" or "Introduction to Cybersecurity" path
- [ ] Solve your first 5 TryHackMe guided rooms
- [ ] Root your first HackTheBox Starting Point machine
- [ ] Complete a full retired HTB Easy machine (recon through root) and write it up properly
- [ ] Participate in at least one live CTF event — [CTFtime.org](https://ctftime.org) keeps a calendar
- [ ] Solve at least one challenge from each major CTF category
- [ ] Build a writeup archive with at least 5 entries

---

### Knowledge Check Items

Can you explain the following?

- What `nmap -sV -sC -p-` does and why each flag is useful
- The difference between a **reverse shell** and a **bind shell**
- What **SUID** means on a Linux binary and why it can be a privesc vector
- How to use `searchsploit` to find public exploits for a known service version
- What a **CVE** is and how you go from CVE number to a working exploit
- The difference between `john` and `hashcat` and when you would use each
- What CyberChef is useful for in a CTF context
- What **GTFOBins** is and how to use it

---

### Relevant Certifications

These align directly with the skills in this section:

- **eJPT** (eLearnSecurity Junior Penetration Tester) — very practical, good first cert
- **CompTIA PenTest+** — vendor-neutral, broader methodology coverage
- **PNPT** (Practical Network Penetration Tester) — report-based exam, no multiple choice, well respected
- **HTB CPTS** — rigorous and lab-heavy, sits roughly at the same level as OSCP

---

### Resources

- [TryHackMe](https://tryhackme.com) — guided paths, good for beginners
- [HackTheBox](https://hackthebox.com) — more autonomous, closer to real work
- [VulnHub](https://vulnhub.com) — free offline VMs, no account needed
- [CTFtime.org](https://ctftime.org) — event calendar and writeup archive
- [IppSec on YouTube](https://www.youtube.com/c/ippsec) — HTB retired machine walkthroughs; watch these after you attempt the box yourself
- [GTFOBins](https://gtfobins.github.io) — Unix binary privesc reference
- [LOLBAS](https://lolbas-project.github.io) — Windows equivalent
- [CyberChef](https://gchq.github.io/CyberChef/) — browser-based data manipulation tool
