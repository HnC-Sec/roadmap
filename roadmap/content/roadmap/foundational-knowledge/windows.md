---
date: '2025-09-27T21:54:37Z'
draft: false
title: 'Basic Windows Knowledge'
weight: 500
topics:
  - Basics of Windows operating system
  - Installing Windows
  - Windows user management
  - Windows package management
  - Basic PowerShell scripting
  - Basic Windows security concepts
milestones:
  - Install and configure a Windows desktop
  - Write a PowerShell script to automate a simple process
knowledge_check:
  - Command Prompt
  - winget, EXE, MSI
  - AD
  - PowerShell ISE
  - Windows Firewall, UAC, Runas
certifications:
  - None
learning_resources:
  - title: "Windows 11 Desktop Administration"
    cost: "Free"
    time: "~3 Hours"
    url: "https://www.youtube.com/watch?v=cDDHSJeBfy8"
    link_text: "YouTube"
    notes: "Basic Windows desktop administration"
  - title: "Windows Server Administration"
    cost: "Free"
    time: "~3 Hours"
    url: "https://www.youtube.com/watch?v=lrtYDS5WKR0&list=PLYogJ_kxL1wTesq-vNxEc8tjDOHvszeWf"
    link_text: "YouTube Playlist"
    notes: "Playlist of about 40 videos covering the basics of Windows Server"
  - title: "Wikiversity: Windows Server"
    cost: "Free"
    time: "Varies"
    url: "https://en.wikiversity.org/wiki/Windows_Server_Administration"
    link_text: "Wikiversity"
    notes: "Various learning modules covering all sorts of Windows Administration topics"
  - title: "Windows Server Administration Fundamentals"
    cost: "Free"
    time: "~6 Hours"
    url: "https://learn.microsoft.com/en-us/shows/Windows-Server-Administration-Fundamentals/"
    link_text: "Microsoft Learn"
    notes: "Great Administration lessons straight from Microsoft"
  - title: "Complete Windows Server Administration"
    cost: "$129"
    time: "15 Hours"
    url: "https://www.udemy.com/course/complete-windows-server-2016-administration-course/"
    link_text: "Udemy"
    notes: "Guided training for Windows Systems Administration"
---

One important milestone in your journey to understanding cybersecurity is gaining a deeper understanding of the Windows operating system. Windows administration is foundational to understanding and securing a wide array of computer systems and networks. 


## Basics of the Windows Operating System

Begin by becoming familiar with Windows' fundamental interface elements. The Desktop serves as your primary workspace, allowing quick access to frequently used files and applications. The Start Menu provides a convenient entry point to launch applications and manage system settings. The Taskbar, located typically at the bottom of your screen, is used to pin frequently accessed applications, switch between open applications, and monitor notifications. File Explorer helps you navigate the file system efficiently, providing an organized view of your files and folders. Finally, the Control Panel gives you comprehensive control over your system's settings and configurations, including managing hardware, software, security, and user preferences.


Understanding file and folder structures is crucial, along with mastering file permissions and basic file operations such as copying, moving, and deleting. It's equally important to become comfortable with common system utilities like Task Manager, which monitors system resources and active processes; Device Manager, for hardware troubleshooting and management; and Event Viewer, which provides detailed logs about system events and issues. Try to spend time working with each utility available in Windows, learning the basic functions of each, along with the various views and options available in each.


## Installing Windows

Becoming proficient in installing Windows involves learning how to create bootable media, such as a USB drive or DVD. Familiarize yourself with the installation process, which includes partitioning drives, configuring system settings, and completing initial setup tasks. As you go through a Windows install, take note of the various options available, and if any of them are unfamiliar to you, make a note to further research them later.


Try installing Windows Server in a VM or on a separate computer. Note the different features available in this version of Windows, along with the different interface and management style. Windows Server is one of the mainstays of the business world, with most companies using common features like Active Directory, Exchange mail server, IIS web hosting, etc. Take time to explore and understand each of the various features, continuing to learn about new network protocols as they come up (e.g., MSTSC/RDP, SMB File sharing, etc.).


## Windows User Management

Effective user management is a cornerstone of system security. Learn how to create and manage user accounts and groups to properly control access levels and permissions. Understanding permissions, privilege escalation risks, and account policies helps safeguard systems against unauthorized access. Understand the difference between local users and groups, and users and groups from an Active Directory domain.


Active Directory is a central service used in Windows networks to manage and authenticate users, computers, and other network resources. It is one of the mainstays of authentication for the business world. It enables centralized management through group policies, which allow administrators to enforce security settings and software installations across multiple computers. Active Directory also maintains computer accounts, allowing systems to join and authenticate securely within the domain. By mastering Active Directory, you gain powerful capabilities in configuration management and can efficiently manage large-scale Windows environments.


## Windows Package Management

Efficiently managing software packages is essential for maintaining system security. Gain proficiency in installing, updating, and removing software through Windows' built-in tools like Microsoft Store and Winget, and also explore popular third-party managers such as Chocolatey. Additionally, understanding and configuring Windows Update is crucial for understanding how a system receives timely security patches and updates. Be prepared to troubleshoot common issues related to software installations and updates to maintain optimal system health.


## Basic PowerShell Scripting

Scripting dramatically improves efficiency in system administration, as well as unlocking many advanced capabilities in Windows that are not available through the GUI. Start by learning PowerShell basics, including command syntax, pipeline usage, and script writing. Take note of the specific way PowerShell names modules in the - format (e.g. Get-Object, Copy-Item, Clear-Variable, etc.). Try developing some simple scripts to automate repetitive tasks, such as user account management, system configuration, and retrieving configurations.


Understanding PowerShell's execution policies and learning best practices for secure scripting are also critical components for safely automating administrative tasks. Not only does this teach you how to properly write secure scripts, but it will introduce you to many of the common mistakes that you might be able to exploit later.


## Common File Types

Windows uses file extensions as a convenient method to indicate the type and associated application of a file. Common examples include .exe for executable programs, .docx for Microsoft Word documents, .xlsx for Excel spreadsheets, .jpg and .png for image files, and .txt for plain text files. File extensions help users quickly identify and open files with the appropriate application.


However, it's important to recognize that file extensions are merely a convenience and not always reliable indicators of a file's true nature. Malicious actors frequently disguise harmful files by altering or falsifying file extensions. Understanding this vulnerability, cybersecurity professionals often analyze the file content itself (such as using tools like hexadecimal editors or specialized software) to confirm the actual file type and ensure security. Learn some of the common methods of identifying a file's true type.


## Basic Windows Security Concepts

Developing a foundational understanding of Windows security concepts is essential preparation for deeper cybersecurity learning. Familiarize yourself with antivirus software, firewall management, and essential security policies to protect systems from threats. Gain practical knowledge of User Account Control (UAC), BitLocker encryption, and basic network security settings. Awareness of common threats and vulnerabilities specific to Windows, such as malware infections and privilege escalation attacks, will significantly enhance your readiness to tackle cybersecurity challenges.


Explore things like the available Group Policy settings and how they interact. If you are feeling bold, dig in and learn about the concept of Windows Access Tokens and impersonation.



