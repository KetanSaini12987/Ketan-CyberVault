# OSI Model Notes

## What is OSI Model?

OSI stands for **Open Systems Interconnection Model**.

It is a conceptual framework used to understand how data travels from one computer to another through a network.

The OSI model contains **7 layers**, and each layer performs a specific function.

---

# OSI Layers (Top to Bottom)

1. Application  
2. Presentation  
3. Session  
4. Transport  
5. Network  
6. Data Link  
7. Physical

---

# Layer 7 — Application Layer

Provides networking services directly to user applications and end users.

Examples:

- Web Browser
- Email Client
- FTP Software
- DNS Requests

Protocols:

- HTTP
- HTTPS
- FTP
- SMTP
- DNS

Function:

- Allows applications to communicate over the network

---

# Layer 6 — Presentation Layer

Responsible for formatting data so the receiving system can understand it.

Functions:

- Data conversion
- Encryption
- Decryption
- Compression
- Decompression

Examples:

- SSL/TLS
- ASCII / Unicode conversion

---

# Layer 5 — Session Layer

Responsible for creating, maintaining, and ending communication sessions between devices.

Functions:

- Session establishment
- Session maintenance
- Synchronization
- Session termination

Example:

- Multiple browser tabs maintaining different sessions

---

# Layer 4 — Transport Layer

Responsible for end-to-end communication and reliable delivery.

Protocols:

- TCP
- UDP

## TCP (Transmission Control Protocol)

Reliable and connection-oriented.

Features:

- Error checking
- Ordered delivery
- Retransmission
- Acknowledgment

Used in:

- Web browsing
- File transfer
- Email

## UDP (User Datagram Protocol)

Fast and connectionless.

Features:

- No guarantee of delivery
- No acknowledgment
- Low latency

Used in:

- Video streaming
- Gaming
- VoIP

Data Units:

- TCP = Segments
- UDP = Datagrams

---

# Layer 3 — Network Layer

Responsible for routing packets to the destination.

Uses logical addressing.

Functions:

- Routing
- Path selection
- IP addressing

Examples:

- IPv4
- IPv6

Example IP:

192.168.1.1

Device:

- Router

---

# Layer 2 — Data Link Layer

Responsible for communication between directly connected devices.

Uses physical addressing.

Functions:

- MAC addressing
- Error detection
- Framing
- Switching

Example MAC Address:

00:1A:2B:3C:4D:5E

Devices:

- Switch
- NIC Card

Note:

MAC addresses are assigned by manufacturer but can be spoofed.

---

# Layer 1 — Physical Layer

Lowest layer of OSI model.

Responsible for transmitting raw bits as signals.

Examples:

- Ethernet Cable
- Fiber Optic
- Wireless Signals
- Electrical Pulses

Devices:

- Hub
- Repeater
- Cables

---

# Easy Mnemonic (Top to Bottom)

All People Seem To Need Data Processing

(Application, Presentation, Session, Transport, Network, Data Link, Physical)

---

# Easy Mnemonic (Bottom to Top)

Please Do Not Throw Sausage Pizza Away

(Physical, Data Link, Network, Transport, Session, Presentation, Application)

---

# Data Flow

## Sending Side

Application → Presentation → Session → Transport → Network → Data Link → Physical

## Receiving Side

Physical → Data Link → Network → Transport → Session → Presentation → Application

---

# Important Commands Related to Networking

## Ping

Used to test connectivity.

ping 8.8.8.8

## Manual Page

man ping

## Traceroute

Shows route packets take to destination.

traceroute google.com

## Whois

Shows domain registration information.

whois google.com

## Dig

DNS lookup tool.

dig google.com  
dig google.com @1.1.1.1  
dig facebook.com ANY

## NSLookup

nslookup google.com  
nslookup -type=NS google.com 8.8.8.8

## Host Command

host -t ns google.com  
host -t mx google.com

## Subfinder

Finds subdomains.

subfinder -d google.com

---

# OSI Layer Device Mapping

| Layer | Device |
|------|--------|
| Application | Proxy |
| Presentation | Gateway |
| Session | Gateway |
| Transport | Firewall |
| Network | Router |
| Data Link | Switch |
| Physical | Hub |

---

# Interview Questions

## Why is OSI model important?

- Helps understand networking
- Helps troubleshooting
- Standard communication model

## Difference between TCP and UDP?

- TCP = Reliable
- UDP = Fast

## Which layer uses IP Address?

- Network Layer

## Which layer uses MAC Address?

- Data Link Layer

---

# Notes

- OSI model is theoretical.
- TCP/IP model is practical and used on the internet.
- Very important for Cyber Security, Networking, and Interviews.

---

# Author

Ketan Saini  
Cyber Security Learning Repository
