# Ignite Room - TryHackMe Writeup

## 🎯 Objective
The goal of this machine is to enumerate a vulnerable CMS (FUEL CMS), exploit it, and gain root access.

---

## 🔍 Enumeration

### Nmap Scan
Performed initial reconnaissance using Nmap:

- Target: 10.10.218.112
- Open ports:
  - 80/tcp (HTTP - Apache 2.4.18 Ubuntu)

Findings:
- Website running **FUEL CMS**
- `/fuel/` directory discovered via robots.txt
- Admin panel exposed at `/fuel`

---

## 🌐 Web Enumeration

Using Gobuster:

- `/assets`
- `/home`
- `/index`
- `/offline`
- `/robots.txt`

Important finding:
- `/fuel` admin panel accessible

---

## ⚙️ CMS Analysis

FUEL CMS version identified: **1.5.2**

Configuration file revealed:
fuel/application/config/database.php
Database credentials found:
- Username: root
- Password: mememe

Admin panel credentials:
- Username: admin
- Password: admin

---

## 💥 Exploitation

Searched for known exploits using Searchsploit and found:

- FUEL CMS Remote Code Execution vulnerabilities

Exploitation approach:
1. Accessed admin panel at `/fuel`
2. Used known vulnerability in FUEL CMS (RCE)
3. Achieved remote code execution on target system

---

## ⬆️ Privilege Escalation

After initial access:

- Used discovered credentials:
su root
password: mememe
- Successfully escalated privileges to root

---

## 🛠️ Tools Used
- Nmap
- Gobuster
- Searchsploit
- Browser
- Linux terminal

---
