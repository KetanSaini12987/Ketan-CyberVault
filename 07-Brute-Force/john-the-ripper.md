# JOHN THE RIPPER

## What is John the Ripper

John the Ripper is a password cracking tool used to crack hashes, encrypted files, and password-protected archives using wordlists, brute-force, and rule-based attacks.

---

## Step 1: Identify Hash Type

Before cracking any hash, first identify its format (MD5, SHA1, SHA256, NTLM, bcrypt, etc.).

### Using hashid

```bash
hashid <your_hash_here>
```

### Using hash-id.py

```bash
cd Downloads
cd hash-identifiers
python3 hash-id.py
```

---

## What is Salting

Salt means random data added to a password before hashing.  
This makes cracking harder and prevents rainbow table attacks.

Example:

```text
password + salt = hashed output
```

---

# Basic John Commands

## Crack MD5 Hash Using RockYou

```bash
john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash_example_file.txt
```

- `raw-md5` = unsalted MD5 hash
- `--wordlist` = password list
- `hash_example_file.txt` = file containing hash

---

## Show Cracked Password

```bash
john --show --format=raw-md5 hash_example_file.txt
```

---

## Auto Detect Hash

```bash
john hash.txt --wordlist=/usr/share/wordlists/rockyou.txt
```

---

## More Examples

```bash
john --format=nt hash.txt --wordlist=/usr/share/wordlists/rockyou.txt
john --format=raw-md5 hash.txt --wordlist=/usr/share/wordlists/rockyou.txt
```

---

# Advanced John Commands

## Multi-Core Attack

```bash
john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt --fork=4 hash.txt
```

- Uses 4 CPU processes

---

## Rule-Based Attack

```bash
john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt --rules hash.txt
```

- Modifies wordlist entries like:

```text
admin → admin123
admin → Admin@
admin → @dmin
```

---

## Incremental (Brute Force)

```bash
john --format=raw-md5 --incremental hash.txt
```

---

## Increase Verbosity

```bash
john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt --verbosity=5 hash.txt
```

---

# Hashcat Alternative

```bash
hashcat -m 0 -a 0 hash.txt /usr/share/wordlists/rockyou.txt
```

- `-m 0` = MD5
- `-a 0` = dictionary attack

---

# Windows Hash Cracking

```bash
john --format=nt --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

- Used for NTLM hashes

---

# Useful Linux Files

## Users List

```bash
cat /etc/passwd
```

## Shadow Password Hashes (Root Required)

```bash
sudo cat /etc/shadow
```

---

# Archive Cracking

## ZIP File

```bash
zip2john file.zip > hash.txt
john hash.txt --wordlist=/usr/share/wordlists/rockyou.txt
```

## RAR File

```bash
rar2john file.rar > hash.txt
john hash.txt --wordlist=/usr/share/wordlists/rockyou.txt
```

---

# TryHackMe Hash Examples

## SHA256 Hash

```text
1C8BFE8F801D79745C4631D09FFF36C82AA37FC4CCE4FC946683D7B336B63032
```

```bash
john --format=raw-sha256 hash.txt --wordlist=/usr/share/wordlists/rockyou.txt
```

---

## bcrypt Hash

```text
$2y$12$Dwt1BZj6pcyc3Dy1FWZ5ieeUznr71EeNkJkUlypTsgbX1H68wsRom
```

### Create 4 Character Wordlist

```bash
grep -E '^.{4}$' /usr/share/wordlists/rockyou.txt > rockyou-4.txt
```

### Crack With Hashcat

```bash
hashcat -m 3200 -a 3 hash.txt ?l?l?l?l
```

- `3200` = bcrypt
- `?l?l?l?l` = 4 lowercase letters

---

## MD4 Hash

```text
279412f945939ba78ce0758d3fd83daa
```

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt --rules --format=raw-md4 hash.txt
```

---

## NTLM Hash

```text
1DFECA0C002AE40B8619ECF94819CC1B
```

```bash
hashcat -m 1000 -a 0 hash.txt /usr/share/wordlists/rockyou.txt
```

---

## SHA512 Crypt Hash

```text
$6$aReallyHardSalt$...
```

```bash
hashcat -m 1800 -a 0 hash.txt /usr/share/wordlists/rockyou.txt --force
```

---

## SHA1 + Salt

```text
e5d8870e5bdd26602cab8dbe07a942c8669e56d6:tryhackme
```

```bash
hashcat -m 160 -a 0 hash.txt /usr/share/wordlists/rockyou.txt --force
```

---

# SSH Private Key Cracking

## Convert Private Key

```bash
ssh2john.py id_rsa > forjohn.txt
```

## Crack Key Password

```bash
john forjohn.txt --wordlist=/usr/share/wordlists/rockyou.txt
```

## Login Using Key

```bash
ssh -i id_rsa user@target_ip
```

---

# LinPEAS + John Workflow

## Upload LinPEAS

```bash
scp linpeas.sh user@target_ip:/dev/shm
```

## Run LinPEAS

```bash
./linpeas.sh
```

## Save Output

```bash
./linpeas.sh | tee linpeas-output.txt
```

If private keys found, crack them using `ssh2john.py`.

---

# Extra Rule Examples

## Wordlist Mutation

```bash
john --format=raw-sha256 --rules=wordlist --wordlist=/usr/share/wordlists/rockyou.txt hash1.txt
```

## Single Rule Mode

```bash
john --rules=single --wordlist=wordlist.txt pdf.hash
```

---

# Notes

- John is best for hashes, ZIP, RAR, SSH keys, PDFs.
- Hashcat is faster when GPU is available.
- Always identify hash type first.
- Use legal labs only.
```
