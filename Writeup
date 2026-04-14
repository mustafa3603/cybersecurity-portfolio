# Gallery - TryHackMe Writeup

## Objective
The goal of this machine is to exploit a web application vulnerability and escalate privileges to root.

---

## Enumeration

### Nmap Scan
Performed initial scanning using Nmap:

- Open ports found:
  - 22/tcp (SSH)
  - 80/tcp (HTTP)

Service detection showed a web server running on port 80.

---

## Web Enumeration

Accessed the website on port 80 and found a simple gallery web application.

Used directory enumeration tools (gobuster/dirsearch) to find hidden directories.

Found an admin panel and upload functionality.

---

## Exploitation

The web application was vulnerable to file upload / weak input validation.

Steps:
1. Uploaded a malicious PHP reverse shell
2. Triggered the shell via browser
3. Got initial foothold on the system

---

## Privilege Escalation (Root)

After gaining access:

- Checked system permissions
- Found misconfigured sudo permissions / weak service configuration
- Exploited local privilege escalation vector
- Gained root access

---

## Tools Used
- Nmap
- Gobuster / Dirsearch
- Burp Suite
- Netcat
- Linux commands

---

## Lessons Learned
- Web file upload vulnerabilities can lead to full system compromise
- Enumeration is the most important step in exploitation
- Always check privilege escalation paths after initial access

---

## Status
✔ Completed
