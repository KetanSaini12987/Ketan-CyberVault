# Hashcat

Hashcat is a password recovery tool used for cracking hashed passwords using GPU acceleration (faster than John the Ripper in most cases).

------------------------------------------------------------

## Basic Syntax

hashcat -m <hash-type> -a <attack-mode> hash.txt wordlist.txt

------------------------------------------------------------

## Attack Modes

0 = Straight (dictionary attack)  
1 = Combination attack  
3 = Brute-force (mask attack)  
6 = Hybrid (wordlist + mask)  
7 = Hybrid (mask + wordlist)

------------------------------------------------------------

## Common Hash Types (-m values)

0     = MD5  
1000  = NTLM  
1800  = SHA512crypt  
3200  = bcrypt  
1400  = SHA256  
22000 = WPA/WPA2  

------------------------------------------------------------

## Examples

MD5 cracking:

hashcat -m 0 -a 0 hash.txt /usr/share/wordlists/rockyou.txt

NTLM cracking:

hashcat -m 1000 -a 0 hash.txt /usr/share/wordlists/rockyou.txt

SHA512 crypt:

hashcat -m 1800 -a 0 hash.txt /usr/share/wordlists/rockyou.txt

bcrypt brute force (4 chars):

hashcat -m 3200 -a 3 hash.txt ?l?l?l?l

------------------------------------------------------------

## Useful Options

--show        = show cracked hashes  
--force       = ignore warnings  
--status      = show progress  
-o file.txt   = save output  
-w 3          = workload tuning (performance)

------------------------------------------------------------

## Mask Attack Syntax

?l = lowercase  
?u = uppercase  
?d = digits  
?s = symbols  

Example:

hashcat -m 0 -a 3 hash.txt ?u?l?l?l?d?d

------------------------------------------------------------

## Important Note

- John = easy & flexible cracking
- Hashcat = fast GPU-based cracking
- Always identify hash type before attacking
