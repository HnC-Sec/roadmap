---
date: '2025-09-28T05:13:33Z'
draft: false
title: 'Basic Networking'
---

---

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

---

To be effective in computer security, it is critical to have a good understanding of basic computer networking. Networking is the foundation of almost all forms of hacking, whether it is over a hard-wired local area network (LAN), a wireless network (WiFi) or the global internet. For most computer systems, the network is the only way to interact with them, and in the world of hacking, it will usually be your primary approach vector to any system. Many of the most common vulnerabilities you will come across are at least in part related to networking, and require a basic understanding of networking to successfully exploit. To launch a successful attack, you need to understand how to craft network packets, interact with network devices, and bypass security measures, all of which relies on having a solid understanding of networking basics.

## The OSI model

The OSI model is a conceptual framework that describes how data is communicated over a network. It is divided into seven layers, each of which has a specific function, and builds upon the services provided by the previous layer. The layers are:

{{% steps %}}

### Physical layer

This layer is responsible for the physical transmission of data over the network medium, such as copper wires, optical fiber, or in the case of wireless networks, the air around us.

### Data link layer

This layer is responsible for framing data into packets and transmitting them reliably over the physical layer. It also includes basic single-link addressing.

### Network layer

This layer is responsible for allowing packets to be addressed to remote systems, and routing packets between systems on different networks.

### Transport layer

This layer is responsible for providing reliable end-to-end communication between applications.

### Session layer

This layer is responsible for establishing, managing, and terminating sessions between applications.

### Presentation layer

This layer is responsible for translating data into a format that can be understood by the receiving application.

### Application layer

This layer is responsible for providing services to applications, such as file transfer, email, and web browsing.

{{% /steps %}}

Many times, students are presented with the OSI model as nothing more than a bit of networking trivia to memorize and regurgitate on command. This method of teaching is usually the result of an incomplete or flawed understanding of the model on the part of the teacher. Understanding the concepts behind the OSI model are key to understanding why the model itself is a critical point of knowledge in networking, and to understanding similar layered models in other spaces. The power of a properly applied layered model like the OSI model is that each layer is almost completely independent of the layers above and below it.

For example, if we look at the physical layer, the entire stack above is built on this layer, but we are easily able to swap out the physical media (fiber, copper, wireless, pigeons) without any changes to the other layers of the stack. Another good example of this is the Networking layer, which includes IP addresses. Right now the internet runs on a mixture of IPv4 and IPv6, which are completely different network layer formats. Because of the layered nature of the OSI model, packets can traverse from IPv4 segments to IPv6 segments and back again, with only the need for a simple translation between the addressing schemes, and all other layers remain completely unaffected.

With this understanding of the model, it opens up a world of possibilities, some useful (FCoE, VxLAN, IPv6 over Bluetooth, Sneakernet), some fanciful (IP over Avian Carrier, IP via Semaphore), but all enabled by the layered nature of the OSI model.

## Basics of addressing

Addressing is another key part of basic networking, and again is critical for being able to understand any network-enabled attack. The primary types of addresses you will encounter in networking are MAC (Media Access Control - Layer 2) and IP (Internet Protocol - Layer 3). The two work in harmony (along with other layers) to ensure that traffic flows smoothly and accurately between devices on networks.

A MAC address is a unique identifier assigned to a network interface controller (NIC) when it is manufactured. It is a 48-bit address that is typically written in hexadecimal format, with six pairs of two digits separated by hyphens. For example, a MAC address might look like this:

`00-11-22-33-44-55`

MAC addresses are used at the data link layer of the OSI model to identify devices on a local network segment. When a device wants to send data to another device on the same network segment, it uses the MAC address of the destination device to address the data packet.

An IP address is a logical address assigned to a device on a network. It is a 32-bit address that is typically written in decimal format, with four groups of three digits separated by periods. For example, an IP address might look like this:

`192.168.1.100`

IP addresses are used at the network layer of the OSI model to identify devices on the internet. When a device wants to send data to another device on the internet, it uses the IP address of the destination device to address the data packet.

In many cases, your computer will be assigned what is known as a "private IP address" in one of the 3 designated blocks of private addresses (`192.168.0.0-192.168.255.255`, `10.0.0.0-10.255.255.255`, `172.16.0.0-172.31.255.255`). These act as an internal-only addressing space that is only unique within a private network such as your home network, or a company's internal network. These addresses are used to move traffic around that smaller network, and are replaced commonly by a public IP address at your router or modem. This service is known commonly as Network Address Translation (NAT).

Note: If you want to be pedantic about it, the proper term for what most people think of as NAT is actually Port Address Translation (PAT), but it will almost always be called NAT regardless.

## Basics of routing and traffic handling

Routing is the process of selecting a path for traffic to travel from one network to another. It is a complex process that can depend on a number of factors, including the network topology, the type of traffic, and the desired performance. Routing is performed by routers, which are network devices that connect two or more networks. Routers use routing tables to determine the best path for traffic to travel. Routing tables contain information about the networks that the router is connected to, as well as the paths to those networks. In addition, many routing tables will contain what is known as a "default route" which is typically going to send traffic to a larger network that can help to direct it where it needs to go, such as from your home network to your ISP (Internet Service Provider).

Traffic handling is the process of managing the flow of traffic on a network. This can involve things like prioritizing traffic, blocking traffic, and redirecting traffic.

## Common protocols and services

Some common protocols and services used on networks include:

### Layer 4 Protocols:

TCP (Transmission Control Protocol): TCP is a transport layer protocol that provides reliable end-to-end communication. It is used for layer 7 protocols such as HTTP, FTP, and SMTP, where data integrity and completeness is more important than speed.

UDP (User Datagram Protocol): UDP is a transport layer protocol that provides unreliable but fast communication. It is used for layer 7 protocols such as DNS and VoIP, where speed is more important than integrity or completeness.

### Layer 7 Protocols:

HTTP (Hypertext Transfer Protocol): HTTP is an application layer protocol that is used to transfer web pages and other resources over the web.

FTP (File Transfer Protocol): FTP is an application layer protocol that is used to transfer files between computers.

SMTP (Simple Mail Transfer Protocol): SMTP is an application layer protocol that is used to send and receive email.

SSH (Secure SHell): SSH is commonly used to connect securely to text-based terminals on remote hosts. Most often it is seen as a method of connecting to a Linux system\'s shell.

## Basic network security

There are a number of basic network security measures that can be implemented to protect networks from attack. These include:

Firewalls: Firewalls are devices that filter traffic between networks and block unauthorized traffic.

Intrusion detection systems (IDS): IDS monitor network traffic for suspicious activity and alert administrators when they detect something suspicious.

Intrusion prevention systems (IPS): IPS are similar to IDS, but they can also take actions to block suspicious traffic.

## Basic network troubleshooting steps

When troubleshooting network problems, it is important to follow a systematic approach. In an ideal world, you would test at each layer of the OSI model, and confirm if that particular layer is functioning and passing data as expected. Some basic troubleshooting steps include:

{{% steps %}}

### Identify

Identify the problem. What exactly is the problem? What are the symptoms?

### Gather

Gather information. What devices are involved in the problem? What software are they running?

### Physical

Check the cables and connections. Make sure that all cables are properly connected and that there are no physical problems.

### Configuration

Check the configuration. Make sure that all devices are configured correctly.

### Restart

Restart the devices. Sometimes restarting the devices can fix the problem.

### Test

Test the network. Once you have made changes, test the network to make sure that the problem has been fixed.
{{% /steps %}}

Here are some resources that can help you to learn more about basic computer networking:

| Title                                   | Cost  | Time      | Link                                                                                                                                                                                                 | Notes                                      |
|------------------------------------------|-------|-----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------|
| Paul Browning - CompTIA A+(Partial)      | Free  | ~5 Hours  | [Youtube](https://www.youtube.com/watch?v=1CZXXNKAY5o&t=71503s)                                                                                                                                    | Module 20 covers Networking                |
| Paul Browning - CompTIA Network+         | Free  | 23+ Hours | [Youtube](https://www.youtube.com/watch?v=xmpYfyNmWbw)                                                                                                                                             | Complete basic Network+ course on Youtube  |
| Basics of Computer Networking            | Free  | ~3 Hours  | [GeeksForGeeks](https://www.geeksforgeeks.org/basics-computer-networking/#)                                                                                                                        | Basics of computer networking. Deep knowledge on some areas |
| Cisco CCNA Training - Keith Barker       | Free  | 20+ Hours | [Youtube](https://www.youtube.com/watch?v=8AX9LandYJU&list=PLQQoSBmrXmrysEaVNia7KVwf85qATIi1V)                                                              | Many videos covering the entire CCNA test material |
| Complete CompTIA Network+ Training       | $20   | 19 Hours  | [Udemy](https://www.udemy.com/course/kevin-netplus/)                                                                                                                                                | Full CompTIA Network+ Course               |
