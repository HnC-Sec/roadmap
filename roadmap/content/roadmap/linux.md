---
date: '2025-09-28T13:51:45Z'
draft: false
title: 'Basic Linux Administration'
---

---

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

---

Linux is an operating system (OS) that can manage your computer's hardware and resources, allowing you to run programs and interact with your device. Unlike Windows or macOS, Linux is open-source, meaning its code is freely available for anyone to modify and distribute. This fosters a vibrant community of developers and enthusiasts who constantly improve and innovate.

## Common Terms

### Distro

Linux distributions (distros) are packaged versions of the Linux kernel, along with additional software and tools tailored for specific needs or user preferences. Popular general-purpose distros include Ubuntu, Fedora, and Mint. Some distros are focused towards specific use cases, such as Kali (penetration testing), Tails (privacy and anonymity), or TrueNAS (shared storage server). Typically what you will find is that distros focused on a single purpose are generally a poor choice for a daily-use desktop OS, either because they have lost flexibility in pursuit of specialty (TrueNAS), or because they are designed to be used as non-persistent environments (Kali, Tails).

### Kernel

The Linux kernel is the core of the operating system. It manages memory, processes, and hardware communication, ensuring everything runs smoothly. Most Linux distros are built on the same open-source kernel, usually just built with slightly different configurations to suit that specific distro's goals. Building and tuning a working binary of the Linux kernel from source has been seen as almost a rite of passage in many Linux circles, since it requires understanding the specific needs of the hardware and software that you are using to be able to select the correct configurations out of the thousands of available options.

### Bootloader

The bootloader is the first program that runs when you start your computer. It locates the kernel and loads it into memory, initiating the boot process. GRUB (GRand Unified Bootloader) is a common bootloader found in many distros.

### Window Manager

The window manager controls how windows appear and behave on your screen. It allows you to resize, move, and minimize windows, creating your preferred workspace layout. Popular window managers include GNOME, KDE, and XFCE. Depending on the window manager, they may have different styles of arranging windows. The most commonly seen style is a Compositing window manager, which draws each window separately and allows for them to be freely moved around. Other styles include Tiling window managers (all windows are arranged on the screen so none of them overlap), or Stacking window managers (all windows are drawn in a "stack" and windows can be moved to the top of the stack).

### Shell

The shell is a text-based interface where you can directly interact with the operating system using commands. It's a powerful tool for experienced users, offering fine-grained control over your system. Most general-purpose distros will default to a GUI (Graphical User Interface), in which you can access a terminal, or shell. Many server-focused and lightweight distros will be shell-only, and won't offer any sort of graphical interface.

This is just a glimpse into the fascinating world of Linux. Remember, the beauty of Linux lies in its flexibility and customization. As you learn more about Linux and try out various different distros and configurations, you will most likely find a specific combination of components that you prefer. Often the selection of specific window managers, shells, editors, and other basic components is a very personal choice, and many Linux enthusiasts feel very strongly about their preferred set of tools (even to the point of causing arguments and holy-wars among users of different opinions).

## Installing Linux

So, you've learned the basics of Linux – its open-source nature, customizability, and powerful command line. But how do you actually get started with this versatile operating system? Well, buckle up, friend, because there's more than one way to skin this penguin.

### Bare Metal: The Purest Experience

Imagine dedicating your entire computer to Linux. That's the bare metal approach – wiping your hard drive clean and installing Linux as the sole OS. This method grants you full access to all your hardware resources and the purest Linux experience.

**Pros:**

- Maximum performance and stability
- Complete control over your system
- No worries about resource conflicts with other OSes

**Cons:**

- Destructive installation (loses existing data)
- Can't easily switch between OSes

### Dual Boot: Sharing the Spotlight

Can't decide between Linux and your current OS (Windows, macOS)? No problem! Dual booting lets you install both OSes side-by-side, choosing which one to boot into at startup. This is a great option for those who need both worlds, like gamers who rely on Windows-specific titles but also want to explore Linux for development or productivity.

**Pros:**

- Maintain access to all applications and data
- Easy switching between OSes
- No virtual machine overhead

**Cons:**

- Requires partitioning your hard drive
- Can be complex to set up initially

### Virtual Machine: The Safe Sandbox

Want to try Linux without committing? Enter the virtual machine (VM). Here, you create a software emulation of a computer within your existing OS, allowing you to install and run Linux in a safe, isolated environment. VMs are perfect for testing software, learning Linux without risking your main system, or simply running incompatible applications.

**Pros:**

- No risk to your existing system
- Easy to isolate and manage
- Can run multiple OSes simultaneously

**Cons:**

- Requires system resources (can impact performance)
- Limited access to hardware compared to bare metal

### Windows Subsystem for Linux (WSL): The Linux Blend

For Windows users curious about Linux, WSL offers a unique blend. It's a compatibility layer within Windows that lets you run native Linux binaries (like command-line tools) directly alongside your Windows applications. Think of it as a lightweight VM focused solely on running Linux essentials.

**Pros:**

- No dual boot or VM setup needed
- Seamless integration with Windows environment
- Access to powerful Linux tools

**Cons:**

- Not a full Linux experience (limited graphical applications)
- Requires Windows 10 or later

**So, which method is right for you?**

It depends on your needs and goals. Bare metal offers the purest Linux experience but requires dedication. Dual booting provides flexibility but involves partitioning. VMs are safe and isolated but resource-intensive. WSL is convenient for Windows users but limited in scope.

Ultimately, the best way to find out is to try them out! Most Linux distributions offer live USB versions you can boot without installation, letting you test drive the OS before committing.

Remember, there's no wrong answer. The beauty of Linux lies in its diversity and flexibility. So, explore your options, choose your path, and welcome to the exciting world of Linux!

## Linux user management

One critical process to understand when using Linux is the idea of user management. You may not think it would be that important, especially if you will be the only person using the system, but there are plenty of times where you may need to create a user to run a specific service under, or to provide specific security controls over a set of resources. One other thing you will hear repeated over and over again when discussing Linux will be repeated here, because I am a strong believer in its validity: You should NEVER be directly logging in to a system as root. If you need to run a specific command with elevated privileges, use something like the sudo command to run it.

**A few useful commands to know**

- `useradd`: Creates new user accounts, specifying usernames, passwords, groups, and other settings.
- `usermod`: Modifies existing user accounts, changing passwords, groups, and other attributes.
- `userdel`: Removes user accounts (beware, data gets deleted too!).
- `groupadd`: Creates new groups.
- `groupmod`: Modifies existing groups.
- `groupdel`: Removes groups (empty groups only!).
- `sudo`: Used to impersonate another user on the system

If you are using a desktop focused distro, you may have access to a graphical user management utility through the system's settings, but it's always good to know how to do the same things through the command line, so that you aren't left high and dry if you are accessing a system remotely through SSH.

## Linux filesystem management

Linux filesystems can be a bit confusing at first, especially if you are used to Windows concepts like drives being separated by letters (C, D, E, etc). A Linux filesystem is all in a single hierarchical layout under the root directory, otherwise known as /. Under this root directory, you will typically find the same basic directories on most Linux systems:

- `/bin`: This is where many of the most common system-wide binary executables will be found, such as ls and cat
- `/boot`: This holds the various files needed to boot your system, such as the kernel image and the bootloader
- `/etc`: This directory usually holds most of the configuration files for system services
- `/home`: This directory holds user's home folders, typically by their username (e.g. /home/javert). The notable exception to this pattern is the root user's home folder, which is usually just /root
- `/lib`: This directory holds various system-wide shared libraries that are used by the binary programs in /bin
- `/tmp`: As you would expect, this directory is designed to be used for temporary storage of files by programs or users. Anything stored in this directory could be deleted at any time, and will usually be purged on each boot of the system
- `/usr`: This directory and it's sub-directories contain most of the user-related programs and data. You will commonly find things like a /usr/lib directory, which is similar to the /lib directory, but for user-installed programs, or a /usr/bin directory, which again is similar to /bin, but for user-installed programs
- `/var`: This directory usually holds the active working files for services. Examples include log files, mail queues, caches, etc.
- `/dev`: This one can be a bit strange to Windows users, but this "directory" holds handles for all the devices on the system

One other major concept to understand is that drives and other filesystems can be "mounted" to points in this file structure. For example, you might mount a network drive to /home/javert/my_network_stuff, which would seem to be under your root filesystem, but in reality, it is it's own filesystem, just attached at that specific path.

## File permissions

- `chown`: Changes the ownership of files and directories.
- `chmod`: Changes the permissions of files and directories.

Understanding Linux permissions is crucial for any user, beginner or pro. Imagine each file as a locked cabinet. Permissions dictate who can open it (read), modify its contents (write), or even execute programs stored within (execute). These permissions are represented by a three-digit code, with each digit controlling access for user, group, and others.

`chmod` stands for "change mode," and it allows you to adjust these permissions. Think of it as tweaking the lock combinations on the cabinet. You can grant or restrict read, write, and execute access for different users and groups, ensuring optimal security and control over your data.

`chown`, on the other hand, stands for "change owner," and it lets you alter the ownership of files and directories. Imagine handing over the master key to a different cabinet owner. This is particularly useful when collaborating with others, as it allows assigning ownership to specific users or groups who require specific access privileges.

Mastering these commands empowers you to manage your Linux system effectively. You can secure sensitive files, share resources securely, and optimize workflow within collaborative environments. Remember, with great power comes great responsibility! Always exercise caution when modifying permissions, ensuring you grant access only to authorized users and maintain the integrity of your system.

## Linux package management

Now you've got your Linux system installed and running, users created, filesystem managed like a pro, but you think to yourself "How do I get more software on here?". The answer to this is usually going to come in the form of a package manager.

Think of a package manager as your personal assistant for software acquisition. It takes care of finding, downloading, installing, updating, and even removing software packages on your system. These packages bundle the program files, configuration settings, and dependencies (additional software required for the program to run) into neat, ready-to-install units.

There are different package managers used across various Linux distributions, each with its own quirks and commands. Some popular ones include:

- `apt` (Debian, Ubuntu): A robust and user-friendly manager with access to vast repositories of software.
- `yum`/`dnf` (Red Hat, Fedora): Powerful managers ideal for system administrators, offering fine-grained control over packages.
- `pacman` (Arch Linux): Simple and efficient, perfect for experienced users who value speed and flexibility.

Using a package manager is incredibly convenient. With a few simple commands, you can:

- Install software: `sudo apt install <program>`
- Update all installed software: `sudo apt update && sudo apt upgrade`
- Remove software: `sudo apt remove <program>`
- Search for software: `apt search`

Package managers also handle dependencies automatically, ensuring all the necessary software is installed alongside your chosen program. No more hunting down missing libraries or dealing with compatibility headaches!

Furthermore, package managers keep your system up-to-date with security patches and bug fixes. Regular updates are crucial for maintaining a stable and secure system, and package managers make this process effortless. You can configure automatic updates or manually check for and apply them at your convenience.

As you progress, there will be times when a package might not exist in your package manager for the software you want to install, and in these cases, you will usually need to build that package from source. This process however goes beyond the scope of a basic Linux tutorial. For the moment, it is enough to know that this is an option.

## Basic Bash scripting

Think of a Bash script as a recipe, where each line represents a step in the process. You tell the script what to do, using commands and syntax similar to what you type directly in the terminal. Once written and saved, the script can be executed, performing the entire sequence of tasks automatically.

But why bother scripting, you ask? The benefits are numerous:

- Automation: Repetitive tasks become effortless. Imagine copying files, backing up data, or sending reports, all triggered by a single script execution.
- Customization: Scripts can be tailored to your specific needs and preferences, automating complex workflows with intricate logic and decision-making.
- Efficiency: Save time and effort by batch-processing tasks instead of manually repeating them.
- Error reduction: Scripts minimize the risk of typos or human error, ensuring consistent and reliable execution.

Getting started with Bash scripting is surprisingly approachable. Here's a glimpse into the basics:

Creating a Script: Any text editor can be used to write your script. Save the file with a .sh extension (e.g., myscript.sh).

Basic Commands: Familiarize yourself with fundamental Bash commands like `echo` (print text), `ls` (list files), `mkdir` (create directories), and `cp` (copy files). These form the building blocks of your scripts.

**Control Flow**: Scripts can make decisions and loop through tasks using keywords like if, else, for, and while. This allows for conditional execution and repetitive actions.

**Variables**: Store data temporarily within your script using variables. Think of them as containers holding values like filenames, numbers, or even text.

**Executing the Script**: Open a terminal, navigate to the script location, and type `bash myscript.sh` (replace myscript.sh with your actual filename). The script will run line by line, performing the specified tasks.

Remember, Bash scripting is a journey, not a destination. Start with simple scripts, gradually adding complexity as you gain confidence. There are abundant online resources, tutorials, and communities to guide you along the way.

## Basic Linux security concepts

Just like a fortified castle, your system needs robust defenses to ward off potential threats and protect its valuable data. Here, we'll explore some essential security practices that form the cornerstones of a secure Linux environment.

### Root

{{< callout type="warning" >}}
Ideally you should never run directly as root
{{< /callout >}}

At the heart of Linux security lies the concept of root. Imagine root as the ultimate administrator, wielding immense power over every aspect of the system. While this power is crucial for system management, granting it carelessly can be disastrous.

This is where sudo comes in. Think of sudo as a trusted advisor to the king (root). Users can request specific privileges using sudo followed by the desired command, but only if authorized by the system configuration. This allows for granular control, granting temporary access to specific tasks without handing over the entire kingdom (root access).

However, even with sudo, caution is key. Never use sudo for routine tasks or grant it to untrusted users. Remember, with great power comes great responsibility!

Another access control mechanism is su, which allows users to temporarily switch to the root user. Think of it as donning a disguise to perform specific tasks requiring root privileges. While convenient in certain situations, su should be used sparingly and only when absolutely necessary. Unlike sudo, su grants full root access, making it a high-risk maneuver.

### IPTables Firewall

Imagine a fortified wall with strategically placed gates – that's essentially what iptables does for your Linux system. It acts as a firewall, filtering incoming and outgoing network traffic based on predefined rules. This helps block unauthorized access attempts, malware communication, and other malicious activities.

iptables configuration can be complex, but its effectiveness in safeguarding your system against external threats is undeniable. Mastering basic iptables rules is a valuable skill for any Linux user concerned about network security.

### SELinux

Beyond firewalls, SELinux adds another layer of defense, acting as a sophisticated security context manager. Imagine it as a vigilant guard who monitors every process and file access, enforcing mandatory access control policies. SELinux can prevent unauthorized actions even if a program gains root privileges, making it a powerful tool for advanced system protection.

While SELinux can be initially daunting, its granular control and proactive approach to security make it a valuable asset for system administrators and security professionals.

Remember: Security is an ongoing process, not a one-time fix. Regularly update your system, install security patches promptly, and implement these essential practices to build a robust defense against potential threats. Your Linux system will thank you for it!

## Container Fundamentals

Containers have revolutionized how applications are deployed and managed in modern Linux environments. Understanding containers is increasingly important for system administrators and security professionals.

**What are Containers?**: Containers are lightweight, portable units that package an application and its dependencies together. Unlike virtual machines, containers share the host operating system's kernel while maintaining isolation between applications.

**Container vs. Virtual Machines**: Containers are more resource-efficient than VMs because they don't require a full operating system for each instance. They start faster, use less memory, and allow for higher density on the same hardware.

**Docker Basics**: Docker is the most popular containerization platform. Key concepts include:
- **Images**: Read-only templates used to create containers
- **Containers**: Running instances of images  
- **Dockerfile**: Text files that define how to build images
- **Registry**: Storage and distribution system for container images

**Container Security Considerations**: Containers introduce new security considerations:
- Container images can contain vulnerabilities
- Privileged containers can compromise host security
- Container networking requires careful configuration
- Secrets and sensitive data need proper handling

**Getting Started**: Begin by installing Docker or Podman on your Linux system and experimenting with basic commands like `docker run`, `docker build`, and `docker ps`. Practice creating simple Dockerfiles and understanding container networking.

## Resources

| Title                                 | Cost  | Time       | Link                                                                 | Notes                                         |
|----------------------------------------|-------|------------|----------------------------------------------------------------------|-----------------------------------------------|
| Differential Diagnosis                 | Free  | Varies     | [Wikipedia](https://en.wikipedia.org/wiki/Differential_diagnosis)    | The basics of differential diagnosis          |
| Troubleshooting Methodologies          | Free  | Varies     | [CompTIA](https://www.comptia.org/blog/troubleshooting-methodology)  | Great overview of the fundamentals of troubleshooting |
| Crucial Steps to IT Troubleshooting    | Free  | 40 Minutes | [Youtube](https://www.youtube.com/watch?v=mIdxo_ymzno)               | Good video covering the steps of troubleshooting |
| Linux System Administrator's Handbook | $45   | Variable   | [Amazon](https://www.amazon.com/gp/product/0131480057)               | Very good Linux system administrator handbook |
| Complete CompTIA Linux+ Training       | $15   | 21 Hours   | [Udemy](https://www.udemy.com/course/complete-linux-training-course-to-get-your-dream-it-job/) | Full CompTIA Linux+ Course                    |
