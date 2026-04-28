╔══════════════════════════════════════════════════════════════╗
║                 JOHN THE RIPPER & HASH CRACKING            ║
╚══════════════════════════════════════════════════════════════╝

[ PURPOSE ]
John the Ripper is a password cracking tool used to recover
passwords from hashes, encrypted archives, SSH keys, and more.

Hashcat is a faster alternative (GPU based) for many hash types.

================================================================
1. HASH IDENTIFICATION
================================================================

Use these tools before cracking to detect hash format.

Command:
hashid <hash>

Example:
hashid 5f4dcc3b5aa765d61d8327deb882cf99

Alternative:
cd Downloads/hash-identifiers
python3 hash-id.py

Common Hash Types:
MD5       SHA1       SHA256       NTLM       bcrypt

Note:
Salting means extra random data is added before hashing.

================================================================
2. BASIC JOHN USAGE
================================================================

Syntax:
john --format=<type> --wordlist=<wordlist> <hashfile>

Examples:

john --format=raw-md5 \
--wordlist=/usr/share/wordlists/rockyou.txt hash.txt

john --format=raw-sha256 \
--wordlist=/usr/share/wordlists/rockyou.txt hash.txt

john --format=nt \
--wordlist=/usr/share/wordlists/rockyou.txt hash.txt

Show cracked password:
john --show hash.txt

================================================================
3. IMPORTANT JOHN OPTIONS
================================================================

--fork=4
Use 4 CPU processes for faster cracking

--rules
Modify words automatically
(admin -> admin123, Admin@1, etc.)

--incremental
Pure brute-force mode

--verbosity=5
Detailed output

Examples:

john --fork=4 hash.txt

john --rules \
--wordlist=/usr/share/wordlists/rockyou.txt hash.txt

john --incremental hash.txt

================================================================
4. HASHCAT QUICK GUIDE
================================================================

Syntax:
hashcat -m <mode> -a <attack> hash.txt <wordlist>

Attack Modes:
-a 0   Dictionary attack
-a 3   Brute force / mask attack
-a 6   Wordlist + suffix mask
-a 7   Prefix mask + wordlist

Common Modes:
-m 0      MD5
-m 1000   NTLM
-m 1400   SHA256
-m 1800   SHA512crypt
-m 3200   bcrypt

Examples:

hashcat -m 0 -a 0 hash.txt rockyou.txt

hashcat -m 1000 -a 0 hash.txt rockyou.txt

hashcat -m 3200 -a 3 hash.txt ?l?l?l?l

================================================================
5. ZIP / RAR PASSWORD CRACKING
================================================================

Extract hash first:

zip2john file.zip > hash.txt
rar2john file.rar > hash.txt

Then crack:

john hash.txt --wordlist=/usr/share/wordlists/rockyou.txt

================================================================
6. SYSTEM FILES (LINUX)
================================================================

cat /etc/passwd
= user accounts list

/etc/shadow
= password hashes (root only)

================================================================
7. TRYHACKME STYLE EXAMPLES
================================================================

[ SHA256 ]

john --format=raw-sha256 \
--wordlist=/usr/share/wordlists/rockyou.txt hash.txt

---------------------------------------------------------------

[ NTLM ]

hashcat -m 1000 -a 0 hash.txt \
/usr/share/wordlists/rockyou.txt

---------------------------------------------------------------

[ bcrypt ]

hashcat -m 3200 -a 3 hash.txt ?l?l?l?l

= tries all 4 lowercase combinations

---------------------------------------------------------------

[ Salted SHA1 ]

File format:
hash:salt

hashcat -m 160 -a 0 hash.txt \
/usr/share/wordlists/rockyou.txt

================================================================
8. SSH PRIVATE KEY CRACKING
================================================================

Convert key:

ssh2john.py id_rsa > keyhash.txt

Crack key:

john keyhash.txt \
--wordlist=/usr/share/wordlists/rockyou.txt

Login after cracking:

ssh -i id_rsa user@ip

================================================================
9. LINPEAS WORKFLOW
================================================================

Run script:

./linpeas.sh

Save output:

./linpeas.sh | tee output.txt

Use it to find:
- weak permissions
- sudo rights
- passwords
- SSH keys
- privilege escalation paths

================================================================
10. QUICK REVISION
================================================================

Detect hash        -> hashid
Crack hash         -> john / hashcat
Show password      -> john --show
ZIP crack          -> zip2john + john
RAR crack          -> rar2john + john
SSH key crack      -> ssh2john + john
Bruteforce         -> --incremental
Word mutations     -> --rules

╔══════════════════════════════════════════════════════════════╗
║                     END OF NOTES                            ║
╚══════════════════════════════════════════════════════════════╝
