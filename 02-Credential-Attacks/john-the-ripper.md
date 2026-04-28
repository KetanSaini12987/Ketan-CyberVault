# John The Ripper & Hash Cracking

## Hash Identification
Check hash type first:

hashid <hash>

OR

cd Downloads/hash-identifiers
python3 hash-id.py

Salting means random extra data is added before hashing.

------------------------------------------------------------

## Basic John Commands

Crack MD5 hash:

john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash.txt

Show cracked password:

john --show --format=raw-md5 hash.txt

General syntax:

john --format=<type> hash.txt --wordlist=/usr/share/wordlists/rockyou.txt

Examples:

john --format=nt hash.txt --wordlist=/usr/share/wordlists/rockyou.txt
john --format=raw-sha256 hash.txt --wordlist=/usr/share/wordlists/rockyou.txt

------------------------------------------------------------

## Useful John Options

Use CPU cores:

john --fork=4 --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash.txt

Use rules:

john --rules --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash.txt

Brute force:

john --incremental hash.txt

Verbose mode:

john --verbosity=5 --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash.txt

------------------------------------------------------------

## Hashcat Alternative

MD5:

hashcat -m 0 -a 0 hash.txt /usr/share/wordlists/rockyou.txt

NTLM:

hashcat -m 1000 -a 0 hash.txt /usr/share/wordlists/rockyou.txt

SHA512 Crypt:

hashcat -m 1800 -a 0 hash.txt /usr/share/wordlists/rockyou.txt --force

bcrypt (4 lowercase letters):

hashcat -m 3200 -a 3 hash.txt ?l?l?l?l

------------------------------------------------------------

## Archive Hash Extraction

RAR:

rar2john file.rar > hash.txt

ZIP:

zip2john file.zip > hash.txt

SSH Private Key:

ssh2john id_rsa > hash.txt

PDF:

pdf2john file.pdf > hash.txt

------------------------------------------------------------

## Linux Enumeration

Users list:

cat /etc/passwd

Run LinPEAS:

./linpeas.sh

Save output:

./linpeas.sh | tee linpeas-output.txt

Copy file through SCP:

scp linpeas.sh user@IP:/dev/shm

------------------------------------------------------------

## Practical Examples

SHA256:

john --format=raw-sha256 hash.txt --wordlist=/usr/share/wordlists/rockyou.txt

MD4:

john --format=raw-md4 --rules --wordlist=/usr/share/wordlists/rockyou.txt hash.txt

Rule based SHA256:

john --format=raw-sha256 --rules --wordlist=/usr/share/wordlists/rockyou.txt hash1.txt

Single rules mode:

john --rules=single --wordlist=wordlist.txt pdf.hash

------------------------------------------------------------

## SSH Key Crack Flow

ssh2john id_rsa > forjohn.txt

john forjohn.txt --wordlist=/usr/share/wordlists/rockyou.txt

ssh -i id_rsa user@IP

------------------------------------------------------------

## Notes

rockyou.txt location:

/usr/share/wordlists/rockyou.txt

John is best for hashes, archives, keys, PDFs.  
Hashcat is faster with GPU support.
