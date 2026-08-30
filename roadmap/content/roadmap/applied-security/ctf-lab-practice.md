---
title: "CTF and Lab Practice"
weight: 10
topics:
  - What CTFs Are and How They're Formatted
  - Building a Lab Environment
  - Core Tooling
  - Approach and Methodology
  - Privilege Escalation Basics
  - OSINT Basics
milestones:
  - Set up a dedicated lab VM running Kali or Parrot OS
  - Complete the TryHackMe "Pre-Security" or "Introduction to Cybersecurity" path
  - Solve your first 5 TryHackMe guided rooms
  - Root your first HackTheBox Starting Point machine
  - Complete a full retired HTB Easy machine (recon through root) and write it up properly
  - Participate in at least one live CTF event
  - Build a writeup archive with at least 5 entries
knowledge_check:
  - "What `nmap -sV -sC -p-` does and why each flag is useful"
  - The difference between a **reverse shell** and a **bind shell**
  - What **SUID** means on a Linux binary and why it can be a privilege escalation vector
  - What a **CVE** is and how you go from a CVE number to a working exploit
  - What **GTFOBins** is and how to use it
certifications:
  - "**eJPT** (eLearnSecurity Junior Penetration Tester) — very practical, good first cert"
  - "**CompTIA PenTest+** — vendor-neutral, broader methodology coverage"
  - "**PNPT** (Practical Network Penetration Tester) — report-based exam, no multiple choice, well respected"
  - "**HTB CPTS** — rigorous and lab-heavy, sits roughly at the same level as OSCP"
learning_resources:
  - title: "TryHackMe"
    cost: "Free / $14 per month for premium"
    time: "Varies"
    url: "https://tryhackme.com"
    link_text: "TryHackMe"
    notes: "Guided paths, good for beginners"
  - title: "HackTheBox"
    cost: "Free / $20 per month for VIP"
    time: "Varies"
    url: "https://hackthebox.com"
    link_text: "HackTheBox"
    notes: "More autonomous, closer to real work"
  - title: "VulnHub"
    cost: "Free"
    time: "Varies"
    url: "https://vulnhub.com"
    link_text: "VulnHub"
    notes: "Free offline VMs, no account needed"
  - title: "CTFtime"
    cost: "Free"
    time: "Varies"
    url: "https://ctftime.org"
    link_text: "CTFtime.org"
    notes: "Event calendar and writeup archive"
  - title: "IppSec"
    cost: "Free"
    time: "Varies"
    url: "https://www.youtube.com/c/ippsec"
    link_text: "YouTube"
    notes: "HTB retired machine walkthroughs; watch these after you attempt the box yourself"
  - title: "GTFOBins"
    cost: "Free"
    time: "Varies"
    url: "https://gtfobins.github.io"
    link_text: "GTFOBins"
    notes: "Unix binary privilege escalation reference"
  - title: "LOLBAS"
    cost: "Free"
    time: "Varies"
    url: "https://lolbas-project.github.io"
    link_text: "LOLBAS"
    notes: "Windows equivalent of GTFOBins"
  - title: "CyberChef"
    cost: "Free"
    time: "Varies"
    url: "https://gchq.github.io/CyberChef/"
    link_text: "CyberChef"
    notes: "Browser-based tool for encoding, decoding, and transforming data"
---

## CTF and Lab Practice

At some point you have to stop reading and start breaking things. CTF (Capture the Flag) competitions and lab environments are where that happens. You will run into real vulnerability classes, make a lot of mistakes, and slowly build a sense for how to approach something you've never seen before.

This section comes first in the Applied Security track because it gives you a low-stakes place to build practical skills before you touch real systems or real programmes.

> **Prerequisite Check:** You should be comfortable in a Linux terminal or Windows command prompt, understand basic networking (ports, protocols, how HTTP works), and have at least some scripting ability. If those feel shaky, work through the Basics sections first.

### What are CTFs?

In a Capture the Flag competition, you find and exploit vulnerabilities to retrieve a "flag" — usually a string like `CTF{something}` that proves you solved the challenge. There are a few common formats:

- **Jeopardy style** — a set of standalone challenges grouped into categories (Web, Crypto, Pwn, Forensics, Reverse Engineering, OSINT, Misc). Most beginner events use this format.
- **Attack/Defence** — teams run identical vulnerable services and attack each other while patching their own. More advanced.
- **King of the Hill** — teams compete to take over, and hold, a single target machine.

HackTheBox and TryHackMe aren't CTFs in the traditional sense, but they serve a similar purpose: intentionally vulnerable machines and labs that teach real techniques in a legal, contained environment.

### Building a Lab Environment

Most people practice from a dedicated attack VM running Kali Linux or Parrot OS, rather than their normal daily-use machine. Tools like VirtualBox or VMware make it easy to run one of these as a virtual machine, isolated from your host system with host-only or NAT networking. Spend some time learning your way around it: where the built-in tools live, how to keep it updated, and how to keep your workspace organized as you go.

### Core Tooling

A handful of tools come up constantly once you start solving challenges:

- `nmap` for port scanning and service enumeration
- `netcat` for connecting to services, testing, and basic shell handling
- `gobuster` or `ffuf` for directory and vhost fuzzing
- `john` and `hashcat` for password cracking
- `Wireshark` for reading packet captures
- CyberChef for encoding, decoding, and data transformation puzzles

You don't need to master all of these before you start. You'll pick each one up naturally as a challenge calls for it.

### Approach and Methodology

Enumerate before you exploit — you can't attack what you haven't found. Take notes as you work, not after; writing things down while they're fresh saves you from re-doing work later, and gives you the raw material for a writeup. Speaking of which, start a personal writeup archive from day one, whether that's a GitHub repo, an Obsidian vault, or a plain text file — whatever you'll actually keep using. Reading other people's writeups is a great way to learn, but only look at one for a box or challenge after it's retired or the event has ended; reading one early just to get a flag defeats the point.

### Privilege Escalation Basics

Most lab machines have two flags: a "user flag" you get from an initial foothold, and a "root flag" (or "system flag" on Windows) you get after escalating your privileges. On Linux, common privilege escalation vectors include SUID binaries, sudo misconfigurations, writable cron jobs, and weak file permissions. On Windows, look out for things like `SeImpersonatePrivilege`, unquoted service paths, and `AlwaysInstallElevated`. Automated enumeration tools like `LinPEAS` and `WinPEAS` will point out likely vectors for you, but they don't catch everything, so it's worth understanding what they're actually checking for.

### OSINT Basics

Open Source Intelligence (OSINT) — gathering information about a target from public sources — comes up in CTFs and carries directly into real-world work. Tools like `whois`, `dig`, and `nslookup` tell you about a domain's registration and DNS records. Google Dorking (using search operators like `site:`, `filetype:`, and `inurl:`) can surface exposed files and pages. `theHarvester` automates gathering emails and subdomains associated with a target.
