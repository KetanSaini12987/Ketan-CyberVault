# Nmap Notes

## What is Nmap?

Nmap (Network Mapper) is an open-source tool used for:

- Network discovery
- Port scanning
- Service/version detection
- OS detection
- Vulnerability scanning
- Firewall evasion testing

It is one of the most important tools in Cyber Security and Penetration Testing.

---

## Useful Resources

- Nmap Dev Mailing List → Latest updates and features
- Sectools.org → Security tools directory

---

# OSI Model (7 Layers)

| Layer | Name | Function |
|------|------|----------|
| 7 | Application | Closest to user, provides network services |
| 6 | Presentation | Encryption, translation, compression |
| 5 | Session | Starts and manages communication sessions |
| 4 | Transport | End-to-end communication (TCP/UDP) |
| 3 | Network | Routing using IP |
| 2 | Data Link | MAC addressing, error-free transfer |
| 1 | Physical | Electrical / hardware transmission |

---

## Basic Syntax

```bash
nmap target
```
Example:
nmap 192.168.1.1

# Target Specification

* Single IP = nmap 1.2.3.4
* Subnet = nmap 1.2.3.4/24
* IP Range = nmap 1.2.3.4-8
* Multiple Hosts = nmap 1.2.3.4 5.6.7.8
* Input from File = nmap -iL hosts.txt
* Domain = nmap example.com

# Port Scanning

* Single Port = nmap target -p80
* Port Range = nmap target -p20-30
* Specific Ports = nmap target -p22,80,443
* Protocol Specific = nmap target -p T:22,U:53
* All Ports = nmap target -p-
* Top Ports = nmap target --top-ports 100

# Scan Techniques 

## Option	Scan Type

-sT	TCP Connect Scan
-sS	SYN Stealth Scan
-sF	FIN Scan
-sX	Xmas Scan
-sN	Null Scan
-sU	UDP Scan
-sA	ACK Scan
-sn	Ping Scan / Host Discovery
-sV	Service Version Detection

## Important Options

* Service Version Detection = nmap -sV target
* OS Detection = nmap -O target
* Verbose Mode = nmap -v target
* Aggressive Scan = nmap -A target

## Includes:

- OS Detection
- Version Detection
- Script Scanning
- Traceroute
- IPv6 Scan
- nmap -6 ipv6_address

## Timing Templates

Option	Name	Speed
-T0	Paranoid	Very Slow
-T1	Sneaky	Slow
-T2	Polite	Slower
-T3	Normal	Default
-T4	Aggressive	Fast
-T5	Insane	Very Fast

* Use T0/T1 for IDS evasion.

# Performance Controls

* Host Timeout = nmap --host-timeout 500ms target
* Scan Delay = nmap --scan-delay 1s target
* Minimum Rate = nmap --min-rate 1000 target

## Output Formats

Option	Format
-oN	Normal Text
-oX	XML
-oG	Grepable
-oA	All Formats

Example:

nmap target -oA results

Creates:

results.nmap
results.xml
results.gnmap

## Host Discovery

* Ping Scan Only = nmap -sn target
* ARP Scan = nmap -PR -sn target/24
* ICMP Echo = nmap -PE -sn target/24
* TCP SYN Ping = nmap -PS22,80,443 -sn target/24
* TCP ACK Ping = nmap -PA80 -sn target/24
* UDP Ping = nmap -PU53 -sn target/24

## DNS Options

* No DNS Lookup = nmap -n target
* Reverse DNS = nmap -R target
* Custom DNS Server = nmap --dns-servers 1.1.1.1 target

## Firewall Evasion

* Fragment Packets = nmap -f target
* Custom MTU = nmap --mtu 16 target
* Source Port Spoofing = nmap --source-port 53 target
* MAC Address Spoofing = nmap --spoof-mac 0 target

# Random MAC.

nmap --spoof-mac Dell target

## Vendor MAC.

- Decoy Scan = sudo nmap -sS -D RND:5 target
- IT uses random decoy IPs.

NSE (Nmap Scripting Engine)

# Scripts location:

/usr/share/nmap/scripts

* Update Script DB = sudo nmap --script-updatedb
* HTTP Headers = nmap --script http-headers target
* Vulnerability Scan = nmap --script vuln target
* SMB Vulnerability Check = nmap --script smb-vuln-ms17-010 target
* HTTP Enum = nmap --script http-enum -p80 target
* Traceroute = nmap --traceroute target

Practical Examples

- Stealth Scan = sudo nmap -sS target
- Xmas Scan Port 21 = sudo nmap -sX -p21 target
- Scan Whole Subnet = nmap 192.168.1.*

Related Tools
- arp-scan = sudo arp-scan -l
- Used to discover live hosts in local network.

## masscan
masscan 10.10.0.0/16 -p80,443 --rate=1000
It is Very fast port scanner.

Notes
Always scan only authorized targets.
Use Nmap in labs, TryHackMe, Hack The Box, or legal environments.
Combine Nmap with Burp Suite, Metasploit, and Wireshark for better results.
Author

Ketan Saini
Cyber Security Learning Repository
