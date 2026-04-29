# NIKTO

## Basic Nikto Scan

```
nikto -h host_ip_address -p port_number -o output_file_name -F file_type
```

- h → target host IP  
- p → port number  
- o → output file name  
- F → output format (txt, html, csv)  

---

## Nikto in Kali (Practical Usage)

### 1. Basic Web Scan

```
nikto -h http://192.168.145.129/dvwa
```

- Scans DVWA web application on target

---

### 2. Save Output to File

```
nikto -h http://192.168.145.129/dvwa -o scan.html
```

- Saves scan results into an HTML report file

---

### 3. Verify Output File

```
ls scan*
```

- Lists generated scan report files

---

### 4. Open Report

```
firefox scan.html
```

- Opens scan report in browser

---

## WHOIS (Domain Information Lookup)

```
whois <domain_name>
```

- Shows domain registrar details  
- Shows registration date  
- Shows expiry date  
- Shows public ownership information  

---

## NSLOOKUP (DNS Query Tool)

### Syntax

```
nslookup OPTIONS DOMAIN_NAME SERVER
```

---

### Example

```
nslookup -type=A tryhackme.com 1.1.1.1
```

---

### DNS Servers

- Cloudflare:
```
1.1.1.1 , 1.0.0.1
```

- Google:
```
8.8.8.8 , 8.8.4.4
```

- Quad9:
```
9.9.9.9 , 149.112.112.112
```

---

### Query Types

| Type  | Description |
|------|-------------|
| A     | IPv4 address records |
| AAAA  | IPv6 address records |
| CNAME | Canonical name records |
| MX    | Mail server records |
| SOA   | Start of Authority |
| TXT   | Text records |

---

## DIG COMMAND

### Syntax

```
dig DOMAIN_NAME
```

```
dig DOMAIN_NAME TYPE
```

```
dig @SERVER DOMAIN_NAME TYPE
```

---

### Examples

```
dig example.com
```

```
dig example.com MX
```

```
dig @8.8.8.8 example.com A
```
