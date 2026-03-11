---
title: "Web Application Security"
weight: 30
---

## Web Application Security

Web applications are the dominant attack surface in modern security work. Whether you are doing bug bounty hunting, a web application penetration test, or a red team engagement, a deep understanding of how web applications are built, and how they break, is essential. This section moves from beginner HTTP fundamentals through to the intermediate exploitation skills required to work on real targets.

> **Prerequisite Check:** You should understand basic networking (HTTP/S, DNS, TCP/IP), be comfortable with browser developer tools, and have completed some CTF-level web challenges before working through this section in depth.

---

### General Topics

**How the Web Works (Beginner)**
- HTTP/S: requests, responses, headers, cookies, status codes
- The browser's role: rendering, JavaScript execution, Same-Origin Policy (SOP), CORS
- How sessions and authentication work: cookies, JWT, OAuth basics
- Web server architecture: reverse proxies, load balancers, CDNs, APIs
- Client-side vs. server-side processing

**Recon and Enumeration**
- Passive recon: Shodan, Censys, `subfinder`, `amass`, `waybackurls`, Google Dorking
- Active recon: virtual host (vhost) fuzzing, directory and parameter enumeration (`ffuf`, `gobuster`, `feroxbuster`)
- Technology fingerprinting: `whatweb`, Wappalyzer, response headers
- JavaScript source analysis: finding hardcoded secrets, endpoints, and logic

**OWASP Top 10 — Core Vulnerability Classes**

The OWASP Top 10 is the industry-standard reference for the most critical web application security risks. Every web security professional needs to understand all ten:

1. **Broken Access Control** — accessing resources or functions you should not be allowed to (IDOR, privilege escalation, path traversal)
2. **Cryptographic Failures** — weak or missing encryption for data in transit or at rest
3. **Injection** — sending untrusted data to an interpreter (SQL injection, command injection, LDAP injection)
4. **Insecure Design** — architectural flaws that cannot be fixed by implementation alone
5. **Security Misconfiguration** — default credentials, unnecessary features enabled, verbose error messages, missing hardening
6. **Vulnerable and Outdated Components** — using libraries or frameworks with known CVEs
7. **Identification and Authentication Failures** — weak passwords, broken session management, missing MFA
8. **Software and Data Integrity Failures** — insecure deserialization, CI/CD pipeline attacks
9. **Security Logging and Monitoring Failures** — insufficient logging to detect or investigate breaches
10. **SSRF (Server-Side Request Forgery)** — making the server issue requests to internal or external resources

**Key Attack Techniques (Intermediate)**
- SQL Injection (manual and with `sqlmap`): error-based, blind, time-based, out-of-band
- Cross-Site Scripting (XSS): reflected, stored, DOM-based — and how to bypass filters
- IDOR (Insecure Direct Object Reference) — finding and escalating access control issues
- SSRF — finding and exploiting internal service exposure
- XXE (XML External Entity) Injection
- CSRF (Cross-Site Request Forgery) and bypass techniques
- Path traversal and file inclusion (LFI/RFI)
- Authentication attacks: credential stuffing, password spraying, session fixation, JWT attacks

**Tooling**
- Burp Suite Community / Pro: intercepting proxy, repeater, intruder, scanner, extensions
- OWASP ZAP as an alternative/complement
- `sqlmap` for automated SQL injection testing
- `ffuf` / `gobuster` for web fuzzing
- Browser developer tools (Network tab, Console, Application storage)

---

### Milestones

- [ ] Intercept, modify, and replay HTTP requests using Burp Suite
- [ ] Exploit a SQL injection vulnerability manually (without sqlmap first)
- [ ] Exploit all three types of XSS (reflected, stored, DOM) in a lab environment
- [ ] Exploit an IDOR vulnerability to access another user's data
- [ ] Exploit an SSRF vulnerability to reach an internal service
- [ ] Complete PortSwigger Web Security Academy labs for at least 5 vulnerability classes
- [ ] Complete the OWASP WebGoat or DVWA setup and exploit all major vulnerability categories
- [ ] Perform a full web application recon workflow against a lab target from scratch

---

### Knowledge Check Items

Can you explain the following?

- The **Same-Origin Policy** and why it exists — and what CORS does to relax it
- The difference between **reflected**, **stored**, and **DOM-based XSS** — and why DOM XSS is harder to detect
- What makes a SQL injection **blind** vs. **error-based** and how you extract data in each case
- What an **IDOR** is and why it is often an access control issue rather than a technical one
- The difference between **authentication** (who you are) and **authorisation** (what you are allowed to do)
- How **JWT** (JSON Web Tokens) work and what common misconfigurations lead to exploitation (alg:none, weak secret, key confusion)
- What **SSRF** is and why it is dangerous in cloud environments (IMDS metadata service exposure)
- How **CSRF** works and what mitigations (SameSite cookies, CSRF tokens) defend against it
- The role of Burp Suite's **Intruder** tool and what it is used for
- What **Content Security Policy (CSP)** is and how it can mitigate (but not fully prevent) XSS

---

### Relevant Certifications

- **eWPT** (eLearnSecurity Web Application Penetration Tester) — practical, lab-based exam
- **BSCP** (Burp Suite Certified Practitioner, PortSwigger) — highly respected, difficult, web-specific
- **OSWA** (Offensive Security Web Assessor) — OffSec's web-focused certification
- **OSCP** — includes web components alongside network exploitation

---

### Recommended Resources

- [PortSwigger Web Security Academy](https://portswigger.net/web-security) — the single best free resource for web security; hands-on labs for every major vulnerability class
- [OWASP Top 10](https://owasp.org/www-project-top-ten/) — official reference documentation
- [OWASP WebGoat](https://owasp.org/www-project-webgoat/) — intentionally vulnerable web application for practice
- [DVWA (Damn Vulnerable Web Application)](https://dvwa.co.uk/) — classic beginner lab
- [HackTheBox Academy — Bug Bounty Hunter Path](https://academy.hackthebox.com/path/preview/bug-bounty-hunter) — structured web security curriculum
- [PentestMonkey SQL Injection Cheatsheet](https://pentestmonkey.net/category/cheat-sheet/sql-injection)
