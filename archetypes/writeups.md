# [Machine/Challenge Name] — Writeup

> **Platform:** Hack The Box / HackSmarter / [Other]
> **Difficulty:** Easy / Medium / Hard / Insane
> **OS:** Linux / Windows
> **IP:** `10.10.10.XXX`
> **Author:** [Your Name]
> **Date:** YYYY-MM-DD
> **Tags:** `#web` `#privesc` `#buffer-overflow` `#active-directory` (etc.)

---

## TL;DR

One or two sentences summarizing the path to root/system/flag — useful for skimmers and for your own future reference.

> *Example: Exploited an unauthenticated file upload on the web app to get a webshell, pivoted through a leaked config file for DB creds, cracked a hash for SSH access, then abused a misconfigured SUID binary to escalate to root.*

---

## Table of Contents

- [Reconnaissance](#reconnaissance)
- [Enumeration](#enumeration)
- [Foothold / Initial Access](#foothold--initial-access)
- [Privilege Escalation](#privilege-escalation)
- [Post-Exploitation](#post-exploitation)
- [Flags](#flags)
- [Lessons Learned](#lessons-learned)
- [Remediation](#remediation)
- [Appendix](#appendix)

---

## Reconnaissance

### Nmap Scan

```bash
nmap -sC -sV -oN nmap/initial.txt 10.10.10.XXX
# Full port sweep
nmap -p- -T4 -oN nmap/allports.txt 10.10.10.XXX
```

**Results:**

| Port | Service | Version | Notes |
|------|---------|---------|-------|
| 22   | SSH     |         |       |
| 80   | HTTP    |         |       |
| 445  | SMB     |         |       |

### Initial Observations

- What stood out immediately (odd port, banner, version, redirect, etc.)
- Hypotheses to test in enumeration

---

## Enumeration

### Web Enumeration (if applicable)

```bash
whatweb http://10.10.10.XXX
gobuster dir -u http://10.10.10.XXX -w /usr/share/wordlists/dirb/common.txt -x php,txt,html
ffuf -u http://10.10.10.XXX/FUZZ -w wordlist.txt
```

**Findings:**
- Directories/endpoints discovered
- Technologies identified (CMS, framework, language)
- Interesting files (backups, `.git`, config files, robots.txt)

### Service-Specific Enumeration (SMB / FTP / SNMP / etc.)

```bash
smbclient -L //10.10.10.XXX -N
enum4linux -a 10.10.10.XXX
```

**Findings:**
- Shares, users, or info leaked
- Credentials found (and where)

### Vulnerability Identification

- CVE / known vuln matched to version banners
- Manual testing that revealed a bug (e.g., SQLi in login form, IDOR, LFI)
- Screenshot or request/response showing the vulnerability

```
[paste relevant HTTP request/response, error message, or PoC output here]
```

---

## Foothold / Initial Access

### Exploitation Steps

1. Step-by-step account of how the vulnerability was leveraged
2. Include exact commands / payloads used
3. Note any trial-and-error that mattered (what *didn't* work and why, if instructive)

```bash
# Example exploit command
python3 exploit.py --target 10.10.10.XXX --lhost 10.10.14.X --lport 4444
```

### Shell Obtained

```
[paste terminal output showing shell access — whoami, id, hostname]
```

**User flag:**
```
[REDACTED or placeholder]
```

---

## Privilege Escalation

### Enumeration for PrivEsc

```bash
# Linux
sudo -l
find / -perm -4000 -type f 2>/dev/null
linpeas.sh

# Windows
whoami /priv
systeminfo
winpeas.exe
```

**Findings:**
- Misconfiguration, vulnerable service, kernel exploit, credential reuse, etc.

### Escalation Path

1. Step-by-step explanation of how you went from low-priv to admin/root/system
2. Commands used

```bash
[commands / exploit code]
```

### Root/System Access Confirmed

```
[paste terminal output — whoami, id]
```

**Root flag:**
```
[REDACTED or placeholder]
```

---

## Post-Exploitation

- Persistence, loot, or additional findings (optional — omit for CTF-only writeups where this isn't relevant)
- Any interesting artifacts found on the box (creds, notes, source code)

---

## Flags

| Flag Type | Value |
|-----------|-------|
| User      | `[REDACTED]` |
| Root/System | `[REDACTED]` |

> Redact real flag values if publishing publicly, per platform rules (HTB and most platforms prohibit posting live flags).

---

## Lessons Learned

- Key techniques or tools that were new to you
- What you'd do differently / faster next time
- Concepts worth revisiting or studying further

---

## Remediation

Brief, professional recommendations as if reporting to a client — this is what separates a writeup from a portfolio piece.

| Vulnerability | Risk | Recommendation |
|----------------|------|-----------------|
| e.g. Unauthenticated file upload | High | Enforce file type validation, authentication, and store uploads outside webroot |
| e.g. Weak SUID binary | High | Remove unnecessary SUID bit or restrict via least privilege |

---

## Appendix

### Tools Used

- nmap, gobuster/ffuf, Burp Suite, linpeas/winpeas, hashcat, etc.

### References

- Links to CVEs, blog posts, or documentation that helped
- (Note: double-check any citation links before including — always good practice to verify sources independently.)

### Full Command Log (optional)

```bash
[paste a raw history/log if you want a complete audit trail]
```