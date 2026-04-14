# Pickle Rick - TryHackMe Writeup

## 🎯 Objective
The goal of this machine is to enumerate a web application, find hidden information, gain access to the system, and escalate privileges to root.

---

## 🔍 Enumeration

### Nmap Scan
Target revealed two open ports:

- 22/tcp → SSH (OpenSSH 8.2p1 Ubuntu)
- 80/tcp → HTTP (Apache 2.4.41)

Website title: **Rick is sup4r cool**

---

### Web Enumeration

Using Gobuster:

Discovered paths:
- `/index.html`
- `/assets`
- `/robots.txt`
- `/server-status` (403)

---

### Fuzzing

Using FFUF:

- `/login` → accessible page
- `/portal` → redirect (302)
- `.php` endpoints tested (restricted access)

---

## 🔐 Information Disclosure

### Source Code Leak

Found in HTML comments:
Username: R1ckRul3s

---

### robots.txt

Found hidden value:
Wubbalubbadubdub

---

## 💥 Exploitation

Using discovered credentials:

- Username: R1ckRul3s
- Password: Wubbalubbadubdub

Access gained to the web portal.

From here, command execution capability was achieved through the web interface.

---

## ⬆️ Privilege Escalation

After gaining initial access:

- Enumerated system
- Identified misconfigured permissions
- Escalated privileges to root using local system misconfiguration

---

## 🛠️ Tools Used
- Nmap
- Gobuster
- FFUF
- Browser
- Linux terminal

---
