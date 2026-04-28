# SMTP (Simple Mail Transfer Protocol)

## What is SMTP?

SMTP stands for **Simple Mail Transfer Protocol**.

It is the protocol used for **sending emails** over a network.

SMTP is responsible for:

- Sending outgoing emails
- Relaying emails between mail servers
- Delivering messages to destination servers

Default Ports:

- 25 = Standard SMTP
- 465 = SMTPS (SSL/TLS)
- 587 = Submission Port (Authenticated SMTP)

---

# SMTP Works With POP3 / IMAP

SMTP handles:

- Sending mail

POP3 / IMAP handle:

- Receiving mail

---

# POP3 (Post Office Protocol v3)

Used to download emails from server to local machine.

Features:

- Downloads inbox locally
- May remove mail from server
- Simpler protocol
- Good for single device use

Default Ports:

- 110 = POP3
- 995 = POP3S

---

# IMAP (Internet Message Access Protocol)

Used to synchronize mailbox with server.

Features:

- Emails remain on server
- Multi-device sync
- Better for mobile + desktop use
- Folder management supported

Default Ports:

- 143 = IMAP
- 993 = IMAPS

---

# SMTP Authentication

Many SMTP servers require:

- Username
- Password
- TLS encryption

Without auth, open relay abuse may happen.

---

# Important SMTP Commands

Used manually through Telnet / Netcat.

HELO  
EHLO  
MAIL FROM  
RCPT TO  
DATA  
QUIT

Example:

telnet target-ip 25

Then:

HELO attacker.com

---

# SMTP Enumeration Commands

Some servers allow user enumeration.

## VRFY

Checks if username exists.

Example:

VRFY admin

## EXPN

Expands aliases / mailing lists.

Example:

EXPN staff

These may reveal valid usernames.

---

# Manual SMTP Enumeration

Connect:

telnet target-ip 25

Then:

VRFY root

If enabled, server may confirm valid user.

---

# Metasploit SMTP Enumeration

Start framework:

msfconsole

Use module:

use auxiliary/scanner/smtp/smtp_enum

Set target:

set RHOSTS target-ip

Use username list:

set USER_FILE /usr/share/seclists/Usernames/top-usernames-shortlist.txt

Run:

exploit

or

run

This may discover valid users.

---

# Install SecLists

sudo apt install seclists

Useful wordlists stored in:

/usr/share/seclists/

---

# Scan SMTP with Nmap

Check service:

nmap -sV -p25 target-ip

Run SMTP scripts:

nmap --script smtp* -p25 target-ip

Common scripts:

smtp-enum-users  
smtp-open-relay  
smtp-commands

---

# Hydra Brute Force Example

If valid username found and another service like SSH exists:

hydra -t 16 -l administrator -P /usr/share/wordlists/rockyou.txt -vV target-ip ssh

Explanation:

hydra = tool  
-t 16 = parallel threads  
-l = username  
-P = password list  
-vV = very verbose  
ssh = target protocol

(Use only in legal labs / authorized systems)

---

# Useful SMTP Ports

25   = SMTP  
465  = Secure SMTP SSL  
587  = SMTP Submission  
110  = POP3  
995  = POP3 Secure  
143  = IMAP  
993  = IMAP Secure

---

# SMTP in Cyber Security

Used in:

- Email server testing
- User enumeration
- Open relay detection
- Credential attacks
- Phishing simulations
- Security audits

---

# Common Risks

- Open relay enabled
- Weak passwords
- User enumeration allowed
- No TLS encryption
- Misconfigured mail server
- Spam abuse

---

# Open Relay

A vulnerable SMTP server that allows anyone to send mail through it.

Can be abused for:

- Spam campaigns
- Phishing
- Malware delivery

---

# Interview Questions

## What is SMTP?

Protocol used to send emails.

## SMTP Default Port?

25

## Difference Between SMTP and IMAP?

SMTP sends mail.  
IMAP receives/syncs mail.

## What does VRFY do?

Checks if username exists.

## What is Open Relay?

SMTP server allowing unauthorized email relay.

---

# Practical Commands

nmap -sV -p25 target-ip

telnet target-ip 25

nc target-ip 25

smtp-user-enum -M VRFY -U users.txt -t target-ip

---

# File Name

SMTP.md

# Folder

01-Networking/SMTP.md

# Author

Ketan Saini  
Cyber Security Learning Repository
