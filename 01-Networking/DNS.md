# DNS Notes (Domain Name System)

## What is DNS?

DNS stands for **Domain Name System**.

It is the system that converts human-readable domain names into IP addresses.

Example:

google.com → 142.250.x.x

Without DNS, we would need to remember IP addresses instead of names.

---

# Why DNS is Important?

- Converts domain names to IP addresses
- Helps users browse websites easily
- Used in email routing
- Used in security monitoring
- Important in reconnaissance and pentesting

---

# Basic Example

When you type:

google.com

Process:

1. Browser asks DNS server
2. DNS server finds IP address
3. Browser connects to server IP
4. Website loads

---

# Common DNS Record Types

## A Record

Maps domain to IPv4 address.

Example:

google.com → 142.250.183.14

---

## AAAA Record

Maps domain to IPv6 address.

---

## MX Record

Mail exchange servers used for email.

Example:

gmail.com mail servers

---

## NS Record

Nameservers responsible for domain.

Example:

ns1.example.com

---

## CNAME Record

Alias record.

Example:

www.site.com → site.com

---

## TXT Record

Stores text data.

Used for:

- SPF
- DKIM
- Domain verification

---

## PTR Record

Reverse DNS lookup.

IP → Domain Name

---

## SOA Record

Start of Authority record.

Contains domain administrative information.

---

# Common DNS Commands

## nslookup

nslookup google.com

nslookup -type=MX gmail.com

nslookup -type=NS google.com

---

## dig

dig google.com

dig google.com MX

dig google.com NS

dig google.com @1.1.1.1

---

## host

host google.com

host -t ns google.com

host -t mx google.com

---

## whois

whois google.com

Used to get domain registration details.

---

# Popular DNS Servers

- 8.8.8.8 = Google DNS
- 8.8.4.4 = Google DNS
- 1.1.1.1 = Cloudflare DNS
- 9.9.9.9 = Quad9 DNS

---

# Common Domain Extensions (TLDs)

## Generic TLDs

- .com = Commercial
- .org = Organization
- .net = Network
- .info = Information
- .biz = Business
- .app = Application
- .shop = Shopping
- .blog = Blog
- .online = Online
- .store = Store
- .xyz = General modern use

---

## Education / Government

- .edu = Educational institutions
- .gov = Government
- .mil = Military

---

## Country Code TLDs (ccTLD)

- .in = India
- .us = United States
- .uk = United Kingdom
- .au = Australia
- .jp = Japan
- .cn = China
- .ru = Russia
- .de = Germany
- .fr = France
- .ca = Canada

---

## Tech / Security Related

- .dev
- .tech
- .cloud
- .ai
- .io
- .security

---

# DNS in Cyber Security

Used in:

- Reconnaissance
- Subdomain Enumeration
- DNS Zone Transfer Testing
- Malware C2 Detection
- Phishing Detection
- Threat Intelligence

---

# Useful Security Tools

## subfinder

subfinder -d google.com

Finds subdomains.

---

## amass

amass enum -d google.com

Advanced subdomain enumeration.

---

## dnsrecon

dnsrecon -d google.com

DNS reconnaissance.

---

# Common DNS Attacks

- DNS Spoofing
- DNS Cache Poisoning
- DNS Tunneling
- Subdomain Takeover
- DNS Amplification DDoS

---

# Interview Questions

## What is DNS?

Converts domain names to IP addresses.

## Difference between A and AAAA record?

A = IPv4  
AAAA = IPv6

## What is MX record?

Used for mail servers.

## What is CNAME?

Alias to another domain.

## What is PTR?

Reverse DNS lookup.

---

# Notes

- DNS is one of the most important internet services.
- Every web request often starts with DNS.
- Strong topic for networking and cybersecurity interviews.

---

# Recommended File Name

DNS.md

---

# Folder Location

01-Networking/DNS.md

---

# Author

Ketan Saini  
Cyber Security Learning Repository
