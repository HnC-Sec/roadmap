---
date: '2026-08-30T00:00:00Z'
draft: false
title: 'Intermediate Computer Networking'
weight: 300
topics:
  - Advanced routing
  - Overlay networking
  - VPNs
  - Intermediate network security
  - Intermediate network troubleshooting
milestones:
  - Understand how traffic is routed on a global scale
  - Configure a multi-site overlay network
  - Understand the security implications of a VPN
  - Troubleshoot complex network issues
knowledge_check:
  - OSPF, BGP
  - VXLan, Tunnel, L2TP
  - Wireguard, OpenVPN, Split-tunnel
  - Port Knocking, Deep Packet Inspection, TLS, MITM, Proxy
certifications:
  - Cisco CCNA/CCNP
learning_resources:
  - title: "Jeremy's IT Lab - Free CCNA"
    cost: "Free"
    time: "~70 Hours"
    url: "https://www.youtube.com/@JeremysITLab"
    link_text: "YouTube"
    notes: "A complete, well-structured CCNA course with labs. Probably the best free networking course available."
  - title: "Practical Networking"
    cost: "Free"
    time: "Varies"
    url: "https://www.practicalnetworking.net"
    link_text: "Practical Networking"
    notes: "Clear written explanations of routing, switching, and TLS. The 'Network Address Translation' and 'TLS' series are excellent."
  - title: "Cisco Networking Academy"
    cost: "Free"
    time: "Varies"
    url: "https://www.netacad.com"
    link_text: "NetAcad"
    notes: "Cisco's own free introductory courses, including Packet Tracer for building virtual labs."
  - title: "GNS3"
    cost: "Free"
    time: "Varies"
    url: "https://www.gns3.com"
    link_text: "GNS3"
    notes: "Network emulator for building multi-router labs with real router images. Heavier than Packet Tracer but far more realistic."
  - title: "Wireshark User's Guide"
    cost: "Free"
    time: "5 Hours"
    url: "https://www.wireshark.org/docs/wsug_html_chunked/"
    link_text: "Wireshark"
    notes: "The official guide. Focus on capture filters, display filters, and the Statistics menu."
  - title: "WireGuard Whitepaper"
    cost: "Free"
    time: "1 Hour"
    url: "https://www.wireguard.com/papers/wireguard.pdf"
    link_text: "WireGuard (PDF)"
    notes: "Short and readable for a protocol paper. A good first security paper to practice on."
  - title: "How Tailscale Works"
    cost: "Free"
    time: "45 Minutes"
    url: "https://tailscale.com/blog/how-tailscale-works"
    link_text: "Tailscale"
    notes: "Excellent explanation of overlay networks, NAT traversal, and mesh VPNs using real-world design."
  - title: "Cloudflare Learning Center - BGP"
    cost: "Free"
    time: "30 Minutes"
    url: "https://www.cloudflare.com/learning/security/glossary/what-is-bgp/"
    link_text: "Cloudflare"
    notes: "Approachable introduction to BGP, autonomous systems, and BGP hijacking."
  - title: "Neil Anderson - Complete Cisco CCNA"
    cost: "~$20"
    time: "~35 Hours"
    url: "https://www.udemy.com/course/ccna-complete/"
    link_text: "Udemy"
    notes: "Well-regarded paid CCNA course with hands-on labs, frequently on sale."
  - title: "TCP/IP Illustrated, Volume 1"
    cost: "~$60"
    time: "Varies"
    url: "https://www.pearson.com/en-us/subject-catalog/p/tcpip-illustrated-volume-1-the-protocols/P200000009312"
    link_text: "Pearson"
    notes: "The reference book for how the protocols actually behave on the wire. Use it as a reference, not a read-through."
---

The foundational networking section covered addresses, subnets, the OSI model, and how a packet gets from one machine to another on a local network. This section scales that up. How does a packet cross the entire internet? How do you build a network that spans several sites and a cloud provider as though it were one LAN? What does a VPN actually protect you from, and what does it not? And when all of it breaks, how do you find out why?

## Advanced Routing

A router decides where to send a packet next by consulting its routing table. On a small network you can fill that table in by hand with **static routes**. That stops working quickly: with dozens of routers and links that fail, you need routers to learn the topology and adapt on their own. That is what a **routing protocol** does.

Routing protocols come in two families, and the distinction matters more than it first appears.

**Interior Gateway Protocols (IGPs)** run *inside* one organization's network. The most common is **OSPF (Open Shortest Path First)**. Every OSPF router floods information about its own links to every other router, so each one builds an identical map of the network. Each then independently runs a shortest-path algorithm over that map to work out its best route to everywhere. Because all routers share the same map, OSPF converges quickly and cannot easily form loops. Large OSPF networks are divided into *areas* to keep the map from growing too big. OSPF's goal is straightforward: find the technically shortest path.

**Exterior Gateway Protocols** run *between* organizations, and in practice there is exactly one: **BGP (Border Gateway Protocol)**. BGP is what holds the internet together. Every large network — an ISP, a cloud provider, a university, a big company — is an **Autonomous System (AS)** with its own number. BGP is how one AS tells its neighbours "these IP ranges are reachable through me", and those announcements propagate outward until everyone knows a path.

BGP is not trying to find the shortest path. It is trying to find the *preferred* path, and preference is set by business relationships, contracts, and policy. A route through a peer you exchange traffic with for free will beat a technically shorter route through a provider you pay. This is the key mental shift: internet routing is a policy system as much as a technical one.

That has a large security consequence. Classic BGP has no built-in way to verify that an AS is entitled to announce the addresses it claims. If an AS announces someone else's address range — by mistake or on purpose — other networks may believe it and send that traffic to the wrong place. This is **BGP hijacking**, and it has been used both to take services offline and to intercept traffic. **RPKI (Resource Public Key Infrastructure)** is the ongoing effort to fix this by cryptographically signing which AS is allowed to announce which prefixes, and adoption is still incomplete.

## Overlay Networking

An **overlay network** is a virtual network built on top of an existing physical one. The physical network (the **underlay**) just moves packets between endpoints; the overlay uses those endpoints to create a network with its own addressing and topology, which need not resemble the physical layout at all.

The mechanism underneath is **tunnelling** — **encapsulation** — where a whole packet is wrapped inside another packet as payload. The outer packet is routed normally across the underlay, and at the far end the wrapper is stripped off and the inner packet is delivered as if it had arrived locally. This is how two machines in different cities can behave as though they are plugged into the same switch.

Some tunnelling technologies you will meet:

- **VXLAN (Virtual Extensible LAN)** — wraps Ethernet frames inside UDP packets. It lets a layer 2 network stretch across a routed layer 3 network, and supports 16 million separate virtual networks. Heavily used in data centres and cloud platforms to give each tenant an isolated network on shared hardware.
- **GRE (Generic Routing Encapsulation)** — a simple, general-purpose tunnel that can carry almost any protocol. No encryption of its own.
- **L2TP (Layer 2 Tunneling Protocol)** — tunnels layer 2 traffic, commonly across the internet. It provides no encryption either, so it is usually paired with IPsec as "L2TP/IPsec".
- **IPsec** — a suite that provides authentication and encryption at the IP layer, and is often the security component under another tunnelling protocol.

Notice the pattern: **encapsulation and encryption are separate things**. Many tunnels give you the first without the second. A tunnel that is not encrypted is still readable by anyone who can see the underlay.

The security implications run in both directions. Overlays give you segmentation — separating environments so that compromising one does not expose the others. They also give attackers a way to hide: tunnelled traffic looks like whatever the outer packet claims to be, which is the basis of many data exfiltration and command-and-control techniques (DNS tunnelling being the classic example).

## VPNs

A **VPN (Virtual Private Network)** is an encrypted tunnel between two points. Two very different use cases share the name, and confusing them causes a lot of bad reasoning about security.

**Remote access VPNs** connect one device to a private network — the classic "working from home into the office" setup, or a commercial privacy VPN service. **Site-to-site VPNs** connect entire networks together, so an office, a data centre, and a cloud environment all behave as one network.

The common implementations:

- **WireGuard** — modern, deliberately small (a few thousand lines of code), fast, and simple to configure. It uses a fixed set of modern cryptographic algorithms rather than negotiating them, which removes a whole category of downgrade attacks. It is now the default choice for most new deployments.
- **OpenVPN** — older, much larger, very flexible, and highly compatible. It runs over TLS and can use TCP port 443, which helps it get through restrictive firewalls.
- **IPsec/IKEv2** — the traditional enterprise standard, built into most operating systems and network hardware, and strong at site-to-site links.

An important configuration choice is **split tunnelling**. With **full tunnelling**, all of a client's traffic goes through the VPN. With **split tunnelling**, only traffic destined for specific networks goes through the tunnel and everything else uses the local internet connection directly. Split tunnelling is faster and reduces load, but it means the device is simultaneously connected to the corporate network and the open internet — which is exactly the bridge an attacker wants. Full tunnelling gives more control and monitoring at the cost of performance.

It is worth being clear about what a VPN actually gives you, because this is widely misunderstood. A VPN protects data **in transit between the two tunnel endpoints**. It does not make you anonymous, it does not protect you from malware, and it does not secure the destination site. It moves your trust: instead of trusting the local network and your ISP, you now trust the VPN provider, who can see everything you do. For a corporate VPN that trade is usually sensible. For a commercial privacy VPN, it is only as good as the provider's honesty and logging policy. Meanwhile, HTTPS already encrypts your web traffic end to end, which covers much of what people buy VPNs to achieve.

From a defender's point of view, VPN concentrators are among the most attacked assets on the internet: they are exposed by definition, they hold credentials, and a compromise puts the attacker inside the network. Several of the most damaging breaches of recent years started at a VPN appliance that had not been patched.

## Intermediate Network Security

At this level, network security stops being "install a firewall" and becomes a set of specific ideas about visibility and trust.

**TLS (Transport Layer Security)** is the protocol behind HTTPS and much else. It provides three things: encryption (nobody can read the traffic), integrity (nobody can alter it undetected), and authentication (you are talking to who you think you are). The authentication part rests on certificates and a chain of trust up to a certificate authority your system already trusts. Understanding the TLS handshake — how the two sides agree on cryptography and prove identity — is one of the highest-value things you can learn at this stage, because so much depends on it.

A **MITM (Man-in-the-Middle) attack** puts an attacker between two parties, able to read and modify traffic while both sides believe they are talking directly. TLS is the main defence, which is why attacks on it — invalid certificates users click through, stripped HTTPS, and compromised certificate authorities — matter so much. The same technique is also used legitimately: an intercepting proxy such as Burp Suite is a deliberate MITM against your own traffic, and it is a core tool for web security testing.

A **proxy** sits between a client and a server and forwards traffic. A *forward proxy* fronts clients, and is used for filtering, caching, and monitoring outbound traffic. A *reverse proxy* fronts servers, and is used for load balancing, TLS termination, and as a place to put a web application firewall. Both are natural chokepoints for inspection, and both are worth understanding as places where traffic can be observed or altered.

**DPI (Deep Packet Inspection)** means looking at packet contents, not just headers. Traditional firewalls decide based on addresses and ports; DPI examines the payload to identify the actual application and to look for known malicious patterns. It is used for intrusion detection, data loss prevention, and application-aware filtering — and by censorship systems. Its main limitation is encryption: DPI cannot read TLS traffic without terminating it, which is why organizations that want full visibility deploy TLS-inspecting proxies, and why that practice is a genuine privacy trade-off rather than an obviously good idea.

**Port knocking** hides a service behind a sequence of connection attempts to closed ports; only after the right sequence does the firewall open the real port for that source address. It is an interesting technique and a good illustration of a broader lesson: it is **obscurity, not security**. The knock sequence is a shared secret sent in the clear, and anyone watching the traffic can replay it. Layered on top of proper authentication it reduces noise and automated scanning; used instead of proper authentication it is a false sense of safety.

The organizing idea behind all of this is **segmentation**: divide the network into zones with controlled paths between them, so that a compromise in one place does not automatically become a compromise everywhere. Flat networks are why a single infected laptop can turn into an organization-wide incident.

## Intermediate Network Troubleshooting

Complex network problems are rarely solved by guessing. They are solved by narrowing down where in the path the behaviour stops matching expectations.

Work the layers deliberately. Is there a physical link? Does the interface have the address and mask you expect? Does the routing table contain a path to the destination, and does the *return* path exist too — one-way routing failures are common and confusing. Does name resolution give the right answer? Does the port accept a connection? Does the application behave correctly once connected? Whether you go bottom-up or top-down matters less than being systematic and writing down what you have ruled out.

Tools worth being genuinely comfortable with:

- `ping` and `traceroute` / `mtr` — reachability and path. Remember that many devices deprioritize or drop ICMP, so an odd hop in a traceroute is often not the problem.
- `dig` — DNS queries, including asking a specific server directly to see whether you have a caching problem or a real one.
- `ss` (or `netstat`) — what is listening locally and what connections exist.
- `tcpdump` and **Wireshark** — the ground truth. When documentation and reality disagree, a packet capture settles it.
- `curl -v` and `openssl s_client` — inspecting HTTP behaviour and TLS handshakes in detail.

Take the time to get good at Wireshark specifically. Display filters, following a TCP stream, reading the handshake, and spotting retransmissions and resets will explain problems that no amount of log reading will. It is also the same skill used in incident response and traffic analysis, so the investment pays twice.

Some recurring causes to keep in mind: MTU problems and blocked ICMP causing large packets to vanish while small ones succeed; asymmetric routing confusing stateful firewalls; NAT hiding the real source address; DNS caching serving stale answers; and a firewall silently dropping traffic rather than rejecting it, which turns a clear error into a hang. Most difficult network problems are boring problems in an unexpected place.
