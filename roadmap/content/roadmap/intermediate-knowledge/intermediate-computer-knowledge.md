---
date: '2026-08-30T00:00:00Z'
draft: false
title: 'Intermediate Computer Knowledge'
weight: 200
topics:
  - Analog vs digital signals
  - Binary encoding
  - Reading RFC/spec documents
  - BIOS vs UEFI
  - RFC2119 Language
  - Basic virtualization
milestones:
  - Read and understand technical spec documents
  - Understand how data is transmitted over analog signals
  - Understand the boot process of a PC
knowledge_check:
  - AM, FM, PM, PCM, QAM
  - (Big/Little)-Endian, bit, nibble, byte
  - BIOS, UEFI, GPT, EFI, Secure Boot
  - MUST, SHOULD, MAY
  - PDU Diagram
  - Hypervisor, VM, Type 1/2 Hypervisor
certifications:
  - None
learning_resources:
  - title: "RFC 2119"
    cost: "Free"
    time: "10 Minutes"
    url: "https://www.rfc-editor.org/rfc/rfc2119"
    link_text: "RFC Editor"
    notes: "The one-page RFC that defines MUST, SHOULD, and MAY. Read it once and you will read every other RFC better."
  - title: "RFC Editor"
    cost: "Free"
    time: "Varies"
    url: "https://www.rfc-editor.org"
    link_text: "RFC Editor"
    notes: "The official archive of every RFC, with search and status (draft, proposed standard, obsoleted)."
  - title: "Code: The Hidden Language of Computer Hardware and Software"
    cost: "~$25"
    time: "~12 Hours"
    url: "https://www.charlespetzold.com/code/"
    link_text: "Charles Petzold"
    notes: "Builds up from a light bulb and a battery to a working computer. The best single book for understanding binary encoding."
  - title: "Ben Eater"
    cost: "Free"
    time: "Varies"
    url: "https://www.youtube.com/c/BenEater"
    link_text: "YouTube"
    notes: "Builds real circuits on breadboards and explains signals, clocks, and buses as he goes."
  - title: "All About Circuits Textbook"
    cost: "Free"
    time: "Varies"
    url: "https://www.allaboutcircuits.com/textbook/"
    link_text: "All About Circuits"
    notes: "Free online electronics textbook. The chapters on AC signals and digital theory cover the analog/digital divide well."
  - title: "RTL-SDR Quick Start Guide"
    cost: "Free (guide) / ~$30 (hardware)"
    time: "2 Hours"
    url: "https://www.rtl-sdr.com/rtl-sdr-quick-start-guide/"
    link_text: "RTL-SDR.com"
    notes: "A cheap USB software-defined radio makes modulation real instead of theoretical. Highly recommended hands-on project."
  - title: "UEFI Specifications"
    cost: "Free"
    time: "Varies"
    url: "https://uefi.org/specifications"
    link_text: "UEFI Forum"
    notes: "The primary source for UEFI and its boot process. Enormous - use it for reference, not for reading end to end."
  - title: "Managing EFI Boot Loaders for Linux"
    cost: "Free"
    time: "2 Hours"
    url: "https://www.rodsbooks.com/efi-bootloaders/"
    link_text: "Rod's Books"
    notes: "Rod Smith's practical explanation of UEFI, the EFI System Partition, and how a machine actually finds its bootloader."
  - title: "VirtualBox Documentation"
    cost: "Free"
    time: "3 Hours"
    url: "https://www.virtualbox.org/manual/"
    link_text: "VirtualBox"
    notes: "Free type 2 hypervisor for any desktop OS. The manual doubles as a decent introduction to virtualization concepts."
  - title: "Proxmox VE Documentation"
    cost: "Free"
    time: "Varies"
    url: "https://pve.proxmox.com/pve-docs/"
    link_text: "Proxmox"
    notes: "Free type 1 hypervisor. Installing it on an old PC is the fastest way to understand bare-metal virtualization."
---

At the foundational level you learned what the parts of a computer are and what they do. This section goes one layer down. It is about how information is physically represented, how the machine gets from powered-off to a running operating system, how to read the documents that define all of this, and how a computer can pretend to be several computers at once.

None of these topics are security topics on their own. All of them turn up constantly in security work, usually at the moment something stops making sense.

## Analog and Digital Signals

An **analog** signal varies smoothly and can take any value in a range. Sound in air, the voltage from a microphone, and a radio wave are all analog. A **digital** signal only takes a small number of defined values — usually two, read as 0 and 1.

Computers are digital, but the world they talk across is analog. Wi-Fi, cellular data, cable internet, and even a copper Ethernet run are all analog signals carrying digital information. Turning bits into a signal is called **modulation**, and turning them back is **demodulation**. The core idea is that you take a steady wave (the *carrier*) and change one of its properties in time with your data.

The main things you can change give the main modulation types:

- **AM (Amplitude Modulation)** — change the height of the wave. Simple, but noise also changes amplitude, so AM is easily corrupted.
- **FM (Frequency Modulation)** — change how fast the wave oscillates. More resistant to noise, which is why FM radio sounds cleaner than AM.
- **PM (Phase Modulation)** — change the timing offset of the wave relative to a reference. Heavily used in digital systems.
- **QAM (Quadrature Amplitude Modulation)** — change amplitude and phase together, so each symbol carries several bits at once. This is what cable internet, Wi-Fi, and modern cellular use to reach high data rates.

**PCM (Pulse Code Modulation)** goes the other direction: it is how an analog signal becomes digital data. You sample the signal's value at a fixed rate and store each sample as a number. An audio CD is PCM at 44,100 samples per second. Sampling is why digital audio has a maximum representable frequency, and why a low sample rate sounds wrong.

Why this matters for security: a great deal of attack surface lives at the radio layer. Car key fobs, garage doors, industrial sensors, Bluetooth devices, and RFID badges all send data over the air, and many of them do it with weak or absent encryption. Understanding modulation is the difference between "there is a signal here" and "I can read and replay this signal". A cheap software-defined radio (SDR) makes this a hands-on subject rather than a theoretical one.

## Binary Encoding

You already know that a **bit** is a single 0 or 1, that 8 bits make a **byte**, and that 4 bits make a **nibble** (which is convenient because one nibble is exactly one hexadecimal digit). The intermediate question is not what these are, but how larger values get laid out in memory and on the wire.

A number bigger than one byte has to be split across several bytes, and there are two ways to order them. **Big-endian** stores the most significant byte first, the way we write numbers by hand. **Little-endian** stores the least significant byte first. The 32-bit value `0x12345678` is stored as `12 34 56 78` in big-endian and `78 56 34 12` in little-endian.

Neither is better, but you must know which one you are looking at. x86 and most ARM systems are little-endian. Network protocols are traditionally big-endian, which is why big-endian is often called *network byte order*. If you have ever stared at a hex dump where a value looked backwards, endianness is why.

Encoding goes beyond numbers. Text has its own layers — ASCII for basic English characters, UTF-8 for essentially everything else — and data is often re-encoded for transport, most commonly with Base64 so that arbitrary bytes can travel through a text-only channel. Base64 is **encoding, not encryption**: it hides nothing, and anybody can reverse it instantly. Confusing the two is a classic beginner mistake, and spotting Base64 in a capture or a log is a routine skill.

Being fluent here pays off directly. Reading raw bytes and recognizing structure in them is the core of file format analysis, protocol reverse engineering, forensics, and exploit development.

## Reading Specifications and RFCs

Eventually the blog posts run out and the only real answer is in a specification. Specifications look unfriendly, but they follow conventions, and once you know the conventions they become the most reliable source you have.

An **RFC (Request for Comments)** is the document format used to define internet standards, published by the IETF and archived at the RFC Editor. Despite the tentative name, RFCs are where HTTP, TCP, DNS, TLS, and most of the internet are actually defined. Each has a permanent number and a status: some are Proposed Standards, some are Informational, and many are **obsoleted** by newer RFCs. Always check the status header before trusting one — reading an obsoleted RFC as though it were current is an easy way to waste a day.

Specifications use precise language, defined by **RFC 2119**. These words are capitalized on purpose:

- **MUST** / **REQUIRED** / **SHALL** — an absolute requirement. An implementation that does not do this is non-compliant.
- **MUST NOT** / **SHALL NOT** — an absolute prohibition.
- **SHOULD** / **RECOMMENDED** — do this unless you have a good, understood reason not to.
- **SHOULD NOT** — avoid this unless you have a good, understood reason.
- **MAY** / **OPTIONAL** — genuinely up to the implementer.

That distinction is a gift to anyone doing security work. Every `SHOULD` is a place where two implementations may reasonably differ, and every `MAY` is a place where they almost certainly do. Differences between implementations of the same specification are the root of whole vulnerability classes, including request smuggling and parser-differential attacks.

Specifications also lean on diagrams. A **PDU (Protocol Data Unit) diagram** shows the layout of a packet or message: a grid, usually 32 bits wide, with each field's position and size marked. Learning to read one and match it against a real packet in Wireshark is one of the most directly useful skills in this section.

Practical advice for reading a specification: don't start at page one. Find the section you need, read the terminology section that defines its words, then read outward until you have enough context. Specifications are reference works, not textbooks.

## The Boot Process: BIOS and UEFI

When you press the power button, the CPU cannot run your operating system yet — it isn't in memory. **Firmware** stored on the motherboard runs first, initializes the hardware, finds a bootloader on a storage device, and hands control to it. The bootloader then loads the operating system kernel.

The old firmware standard is the **BIOS (Basic Input/Output System)**. It starts the CPU in 16-bit mode, reads the first 512-byte sector of a disk (the Master Boot Record, or MBR), and executes it. That tiny space is why MBR bootloaders are so cramped, and the MBR partition scheme caps disks at 2 TB with at most four primary partitions.

The modern replacement is **UEFI (Unified Extensible Firmware Interface)**. It works differently in ways worth knowing:

- It uses **GPT (GUID Partition Table)** instead of MBR, removing the size and partition-count limits.
- Bootloaders are ordinary `.efi` files sitting in a normal FAT filesystem on the **EFI System Partition (ESP)**, rather than raw sectors. You can list them with a file manager.
- The firmware keeps a boot entry list in non-volatile memory, so multiple operating systems can be registered properly.
- It runs in 32- or 64-bit mode and offers far richer services, including a pre-boot shell and network stack.

**Secure Boot** is a UEFI feature that checks the cryptographic signature of each bootloader before running it, against keys held in firmware. Its purpose is to stop a **bootkit** — malware that loads before the operating system and can therefore hide from it. Anything that runs before your defences is extremely hard to detect afterwards, which is why this layer gets so much attention from both attackers and defenders.

The security relevance is broad: firmware-level persistence, evil-maid attacks against unattended laptops, disk encryption (which needs the bootloader to unlock the disk before the OS exists), and forensic imaging all require you to understand what happens before the operating system starts.

## Basic Virtualization

**Virtualization** lets one physical machine run several isolated operating systems at the same time. The software that manages this is a **hypervisor**, and each guest operating system runs in a **virtual machine (VM)** with virtual CPUs, memory, disks, and network cards.

There are two kinds:

- A **type 1 (bare metal) hypervisor** runs directly on the hardware, with no host operating system underneath. VMware ESXi, Proxmox VE, Microsoft Hyper-V, and Xen are examples. This is what data centres and cloud providers run.
- A **type 2 (hosted) hypervisor** runs as an application inside a normal operating system. VirtualBox, VMware Workstation, and QEMU used casually are examples. This is what you run on your laptop.

The line is blurrier than it used to be — KVM turns a Linux kernel into a type 1 hypervisor while Linux still behaves like a normal OS — but the distinction is still a useful way to think about where the hypervisor sits.

Containers (Docker and friends) are related but not the same thing. A VM virtualizes hardware and runs its own kernel; a container shares the host kernel and only isolates the process environment. Containers are lighter and start faster, but the isolation boundary is thinner.

For security work, virtualization is essential infrastructure. It gives you a disposable lab where you can detonate malware, run vulnerable targets, and snapshot a machine before an experiment so you can roll it back afterwards. It is also a security topic in its own right: a **VM escape**, where code inside a guest breaks out into the hypervisor or another guest, is one of the most serious vulnerability classes there is, because the entire multi-tenant cloud model depends on that boundary holding.
