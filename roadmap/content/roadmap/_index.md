---
aliases:
- /from-power-button-to-pwn-a-roadmap-to-computer-security
date: '2025-09-25T16:47:05Z'
draft: false
title: 'From Power Button to PWN - A Roadmap to Computer Security'
---

## Introduction

Very often I have been confronted by beginners, just realizing the vast playground that is modern technology, with statements like “I’m interested in computers and security”, or “I want to get into bug bounties”, or even “I want to learn to hack”, usually followed by “How do I get there?”. This article, along with others linked from the various sections, aims to be a basic roadmap that can be referenced by learners on the path to learning about the vast world of computer security. The roadmap provides some various signposts, guidance, and milestones along the way, but by design is not a comprehensive guide. 

One statement that anyone who has seen me respond to this type of question has seen is “[Hacking/Security] is almost always going to be 90% learning, and 10% doing. If you pursue this path, you will often find yourself spending hours researching, reading documentation, reviewing code, or slogging through academic papers, looking for the small nuggets that can carry you forward to the next step. If you have an aversion to learning, maybe this isn’t the right path for you.” I will absolutely reiterate that here, as it has been my experience in spending the last 30 years being an independent learner in the space, and it has helped me to build a vast foundation of knowledge that can help to understand complex problems and situations, with enough depth to quickly dive in and learn more.

> [Hacking/Security] is almost always going to be 90% learning, and 10% doing. If you pursue this path, you will often find yourself spending hours researching, reading documentation, reviewing code, or slogging through academic papers, looking for the small nuggets that can carry you forward to the next step. If you have an aversion to learning, maybe this isn’t the right path for you.

In creating this document, I will aim to keep things in a mostly linear order, with topics building on what has come before. If you can look at the knowledge check items in a section and say “I know what all of that is, and the basics of how it works”, feel free to skip that section. If you find that later you are noticing items you don’t have an understanding of, you might want to go back and brush up a bit before continuing. 

Generally I find that in learning, it is best to go through each topic, and if you are presented with terms or concepts that you don’t know or understand, stop and make note of where you are, go spend a few minutes researching and learning the basics of whatever you are missing, then return to your original training and see if it makes more sense in light of new information. This ensures a solid foundation of knowledge for your future learning and exploring, and it transforms what might have otherwise been a straight and narrow learning path into a resilient web of knowledge for you to build on.

Each section will have the same basic layout:

- General Topics – These are the topics you are aiming to understand in this section
- Knowledge Check Items – These are all specific terms, concepts, or acronyms you should know and understand before moving on to future sections
- Milestones – These are tasks or exercises that can be done to provide some practical experience with knowledge from this section, or things that you should feel comfortable doing
- Relevant Certifications – These are going to be any relevant certifications that will cover the same learning area

## Overview and Outline

Below is the basic outline of the learning plan. As I am able to flesh out sections, they will include links to other articles with further details and recommendations.

## Foundational Knowledge
### Basic Research and Learning

**General Topics**

- How to find resources
- How to evaluate a source
- How to ask questions
- Identifying bias and scams
- Using AI for learning
- Types of sources

**Milestones**

- Find reliable source material on a topic
- Ask questions intelligently to avoid XY problems
- Identify likely bias and false information

**Knowledge Check Items**

- Google, Google Scholar
- Clickbait, Content Farm
- The XY Problem
- Types of Bias
- AI Hallucination

**Relevant Certifications**

- None

## Basic Computer Knowledge
### [Basic Computer Hardware and Software](hardware)

**General Topics**

- Basic computer hardware components
- Common interfaces and standards
- Binary and Binary logic
- Common computer formats

**Milestones**

- Build a desktop PC from components
- Install an Operating System

**Knowledge Check Items**

- CPU, RAM, SSD, HDD, GPU, PCI, HDMI
- Boolean logic (AND, OR, NOT, NOR, NAND, XOR)
- Operating System (Windows, Linux, Unix, Android, iOS, MacOS)
- SOC (System on a Chip), Embedded Device

**Relevant Certifications**

- CompTIA A+

### [Basic Computer Networking](networking)
**General Topics**

- The OSI model
- Basics of addressing
- Basics of routing and traffic handling
- Common protocols and services
- Basic network security
- Basic network troubleshooting steps

**Milestones**

- Set up a basic network
- Identify and implement basic network security

**Knowledge Check Items**

- A.P.S.T.N.D.P. / P.D.N.T.S.P.A.
- MAC Address, IP Address, Subnet Mask, CIDR, IPv4, IPv6
- Switching, Routing, Ethernet, 802.11, NAT, PAT
- TCP, UDP, HTTP, SSH, DNS, DHCP
- Firewall, IDS, IPS, VLAN
- Ping, Traceroute, Wireshark, Latency, Packet Loss

**Relevant Certifications**

- Cisco CCNA
- CompTIA Network+

### Basic Linux Administration
**General Topics**

- Basics of Linux operating system
- Installing Linux
- Linux user management
- Linux filesystem management
- Linux package management
- Basic Bash scripting
- Where Linux came from
- Basic Linux security concepts

**Milestones**

- Install and configure a simple Linux OS (Ubuntu, Fedora, Mint, etc)
- Write a bash script to automate a simple process

**Knowledge Check Items**

- Distro, Kernel, Bootloader, Window Manager, Shell, GRUB
- Shadow file, Hard Link, Symbolic Link
- Man page
- Package Manager (YUM, APT, DNF, dpkg, rpm)
- UNIX, GNU
- Sudo, su, iptables, selinux

**Relevant Certifications**

- CompTIA Linux+
- Linux Foundation LFCS
- Redhat RHCSA

### [Basic Windows Knowledge](windows)
**General Topics**

- Basics of Windows operating system
- Installing Windows
- Windows user management
- Windows package management
- Basic PowerShell scripting
- Basic Windows security concepts

**Milestones**

- Install and configure a Windows desktop
- Write a PowerShell script to automate a simple process

**Knowledge Check Items**

- Command Prompt
- winget, EXE, MSI
- AD
- PowerShell ISE
- Windows Firewall, UAC, Runas

**Relevant Certifications**

- None

### [Basic Troubleshooting](troubleshooting)
**General Topics**

- How to read error messages
- Different troubleshooting strategies
- Common types of diagnostic data
- Common sources of troubleshooting information

**Milestones**

- Identify, diagnose, and fix simple issues
- Locate a program’s log files
- Read a stack trace and identify the source
- Intelligently locate known fixes

**Knowledge Check Items**

- Stack Trace, Process ID
- AppData, /var/log
- Event viewer, journalctl, dmesg
- Knowledge Base, Documentation, Community

**Relevant Certifications**

- None

### Basics of Programming
**General Topics**

- Language syntax
- Basic flow control
- Variable types
- Comparison operators
- Basic code layout and flow
- Compiling/Executing code
- Debugging
- Library management
- Object Oriented Programming

**Milestones**

- Develop a simple program in one language
- Debug basic issues and errors in one language
- Create a basic object design for a common concept

**Knowledge Check Items**

- If, Then, Else, While, For, For Each
- Object Oriented Programming, Functional Programming
- Integer, Floating Point, String, Array, Dictionary, Hashtable, Object
- Recursion
- Compiler, Interpreter, Debugger
- Break point
- Inheritance, Abstraction, Duck Typing

**Relevant Certifications**

- None

### Basics of Ethical Hacking and Cyberlaw
**General Topics**

- What is and isn’t Ethical Hacking
- How to identify local laws
- What is a Bug Bounty program
- Ownership and consent

**Milestones**

- Identify ethical vs unethical hacking
- Determine appropriate rules of engagement
- Locate and understand bug bounties
- Avoid accidentally breaking the law

**Knowledge Check Items**

- EULA, ToS
- CFAA, SCA, ECPA, DTSA, GDPR
- Service Ownership vs Content Ownership
- Rules of Engagement
- White hat, black hat, grey hat
- Ignorance as a defense

**Relevant Certifications**

- EC Council CEH
- CompTIA Security+

## Intermediate Knowledge
### Intermediate Research and Learning
**General Topics**

- Finding deeper resources
- Synthesizing knowledge
- Finding and reading academic research

**Milestones**

- Find and understand academic research
- Infer details from incomplete data
- Research deeper learning techniques independently

**Knowledge Check Items**

- Metasearch engine
- Search operators
- Boolean queries
- Professional Networking

**Relevant Certifications**

- None

### Intermediate Computer Knowledge
**General Topics**

- Analog vs digital signals
- Binary encoding
- Reading RFC/spec documents
- BIOS vs UEFI
- RFC2119 Language
- Basic virtualization

**Milestones**

- Read and understand technical spec documents
- Understand how data is transmitted over analog signals
- Understand the boot process of a PC

**Knowledge Check Items**

- AM, FM, PM, PCM, QAM
- (Big/Little)-Endian, bit, nibble, byte
- BIOS, UEFI, GPT, EFI, Secure Boot
- MUST, SHOULD, MAY
- PDU Diagram
- Hypervisor, VM, Type 1/2 Hypervisor

**Relevant Certifications**

- None

### Intermediate Computer Networking
**General Topics**

- Advanced routing
- Overlay networking
- VPNs
- Intermediate network security
- Intermediate network troubleshooting

**Milestones**

- Understand how traffic is routed on a global scale
- Configure a multi-site overlay network
- Understand the security implications of a VPN
- Troubleshoot complex network issues

**Knowledge Check Items**

- OSPF, BGP
- VXLan, Tunnel, L2TP
- Wireguard, OpenVPN, Split-tunnel
- Port Knocking, Deep Packet Inspection, TLS, MITM, Proxy

**Relevant Certifications**

- Cisco CCNA/CCNP

### General Security
**General Topics**

- The CIA Triad
- Authorization vs Authentication
- Threat Modeling
- Risk and Vulnerability Management
- Incident Response
- Auditing

**Milestones**

- Understand the tradeoff of various security measures
- Determine if a control is related to authz or authn
- Create a threat profile and address each threat
- Understand common audit frameworks and requirements

**Knowledge Check Items**

- Confidentiality, Integrity, Availability
- Authz, Authn, RBAC, ABAC, MFA
- Threat, Threat Profile, Asset, Agent, Control
- Mitigate, Eliminate, Transfer, Accept, Compensating Control
- CSIRT, IRP
- ISO, PCI-DSS, HIPAA, SOX

**Relevant Certifications**

- CompTIA Security+
- ISC² CISSP


## Advanced Knowledge

Coming Soon!
Special Thanks

Special thanks to the following server members for helping in the creation and expansion of this roadmap

- ser3n1ty
