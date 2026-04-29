# NMAP (Network Mapper)

## 1. Resources & References
- nmap-dev mailing list → Updates & new features  
- http://sectools.org → Alternative tools & comparisons  

---

## 2. OSI Model (For Nmap Understanding)

| Layer | Name | Function |
|------|------|----------|
| 7 | Application | User-facing services (HTTP, FTP, SSH) |
| 6 | Presentation | Encryption, compression, encoding |
| 5 | Session | Manages sessions between systems |
| 4 | Transport | TCP/UDP communication, segmentation |
| 3 | Network | IP routing & packet delivery |
| 2 | Data Link | MAC addressing, error detection |
| 1 | Physical | Physical transmission (cables, signals) |

---

## 3. Target Specification

| Type | Example |
|------|--------|
| Single IP | nmap 192.168.1.1 |
| Subnet | nmap 192.168.1.0/24 |
| Range | nmap 192.168.1.1-50 |
| Multiple IPs | nmap 1.1.1.1 2.2.2.2 |
| File input | nmap -iL targets.txt |
| Domain | nmap example.com |

---

## 4. Port Scanning Options

| Type | Command |
|------|--------|
| Single port | -p80 |
| Port range | -p20-30 |
| Multiple ports | -p22,80,443 |
| All ports | -p- |
| Top ports | --top-ports 100 |
| TCP + UDP | -p T:22,U:53 |

---

## 5. Scan Techniques

| Type | Option |
|------|--------|
| TCP Connect | -sT |
| SYN Scan (Stealth) | -sS |
| FIN Scan | -sF |
| Xmas Scan | -sX |
| Null Scan | -sN |
| UDP Scan | -sU |
| ACK Scan | -sA |
| Ping Scan | -sP |
| Version Detection | -sV |

---

## 6. Timing & Performance

| Level | Name | Usage |
|------|------|------|
| T0 | Paranoid | Extremely slow, IDS evasion |
| T1 | Sneaky | Slow scan |
| T3 | Normal | Default balanced scan |
| T4 | Aggressive | Fast scan (recommended) |
| T5 | Insane | Very fast, less accurate |

### Extra Controls
- --host-timeout 500ms → skip slow hosts  
- --scan-delay 1s → delay between packets  

---

## 7. Output Formats

| Option | Format |
|------|--------|
| -oN | Normal text |
| -oX | XML format |
| -oG | Grepable format |
| -oS | Script kiddie format |

---

## 8. Host Discovery (Ping Methods)

| Method | Command |
|------|--------|
| ARP Scan | -PR |
| ICMP Echo | -PE |
| ICMP Timestamp | -PP |
| ICMP Mask | -PM |
| TCP SYN Ping | -PS |
| TCP ACK Ping | -PA |
| UDP Ping | -PU |

---

## 9. Firewall Evasion Techniques

- iptables -I INPUT -p tcp --dport 22 -j DROP → block SSH scan  
- --spoof-mac → fake MAC address  
- -D RND:5 → decoy scan  
- -f → packet fragmentation  
- --mtu 16 → custom fragmentation  
- -sI → idle zombie scan  
- --source-port 53 → bypass firewall rules  

---

## 10. Nmap Scripting Engine (NSE)

### Script Examples
- --script http-headers → fetch HTTP headers  
- --script vuln → vulnerability scanning  
- --script smb-vuln-ms17-010 → SMB exploit check  
- --script http-enum → directory enumeration  
- --script ftp-brute → FTP brute force  
- --script discovery → run discovery scripts  

### Script Directory
- /usr/share/nmap/scripts/

---

## 11. DNS Options

| Option | Purpose |
|------|--------|
| -n | No DNS resolution |
| -R | Force reverse DNS |
| --dns-servers | Use custom DNS |

---

## 12. Advanced Scanning Techniques

- -f → packet fragmentation  
- --mtu 16 → manual fragmentation  
- -sI → zombie scan  
- --source-port 53 → firewall bypass  

---

## 13. Masscan vs ARP Scan

| Tool | Purpose |
|------|--------|
| arp-scan | Local network discovery |
| masscan | Extremely fast port scanning |

### Examples
- arp-scan -l  
- masscan 192.168.1.0/24 -p80,443 --rate=1000  

---

## 14. Metasploit Zombie Scan Workflow

1. msfconsole  
2. use auxiliary/scanner/ip/ipidseq  
3. set RHOSTS <range>  
4. run  

Then:
- nmap -sI <zombie_ip> <target_ip>

---

## 15. Summary Cheatsheet

| Task | Command |
|------|--------|
| Host discovery | nmap -sn |
| Full scan | nmap -sS -p- |
| Version detection | nmap -sV |
| OS detection | nmap -O |
| Aggressive scan | nmap -A |
| No DNS | nmap -n |
