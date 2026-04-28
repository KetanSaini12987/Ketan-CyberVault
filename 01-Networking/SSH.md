# SSH (Secure Shell)

## What is SSH?

SSH stands for **Secure Shell**.

It is a secure protocol used to remotely connect and manage another machine over a network.

Default Port: **22**

Used for:

- Remote Login
- Server Administration
- Secure Command Execution
- File Transfer
- Tunneling
- Pentesting

---

# Basic SSH Login

ssh username@ip-address

Example:

ssh root@192.168.1.10

If first time connecting:

yes

Then enter password.

Disconnect:

exit

or

Ctrl + D

---

# Login Using Private Key

ssh -i keyfile username@ip

Example:

ssh -i id_rsa cappucino@10.10.210.234

- -i = private key file

---

# Check SSH Location

which ssh

Example Output:

/usr/bin/ssh

---

# Check SSH Package

apt search openssh-client

---

# Useful Linux Commands

## Show Home Directory Files

ls /home -a

- -a = hidden files also

## Show SSH Folder

ls ~/.ssh

---

# SSH Config File (Use Alias Instead of IP)

Go to SSH folder:

cd ~/.ssh
touch config
nano config

Add:

Host bruce
    HostName 192.168.xx.xx
    Port 22
    User root

Multiple Hosts:

Host server2
    HostName 172.xx.xx.xx
    Port 22
    User kali

Connect:

ssh bruce

---

# Generate SSH Keys

ssh-keygen

Default path:

~/.ssh/id_rsa

Files created:

id_rsa      = Private Key
id_rsa.pub  = Public Key

Check:

cd ~/.ssh
ls -l

---

# Passwordless Login (Manual Method)

## View Public Key

cat ~/.ssh/id_rsa.pub

Copy full key.

## Login Remote Server

ssh root@ip-address

## Create SSH Folder

mkdir -p ~/.ssh
nano ~/.ssh/authorized_keys

Paste copied public key.

Logout:

exit

Now reconnect:

ssh root@ip-address

No password required.

---

# Easy Method

ssh-copy-id -i ~/.ssh/id_rsa.pub root@ip-address

Then:

ssh root@ip-address

---

# Generate Modern Secure Key

ssh-keygen -t ed25519 -C "acme"

Options:

- -t = key type
- ed25519 = modern secure algorithm
- -C = comment

Save as:

~/.ssh/acme_id_ed25519

---

# SSH Agent

Used to store passphrase in memory.

Check running agent:

ps aux | grep ssh-agent

Start agent:

eval "$(ssh-agent)"

Add key:

ssh-add ~/.ssh/acme_id_ed25519

---

# Common SSH Options

## Custom Port

ssh -p 2222 user@ip

## Verbose Mode

ssh -v user@ip

## Extra Verbose

ssh -vvv user@ip

---

# SCP (Secure Copy)

Copy file to remote:

scp file.txt user@ip:/home/user/

Copy from remote:

scp user@ip:/etc/passwd .

---

# SSH in Cyber Security

Used for:

- Remote Shell
- Linux Labs
- Privilege Escalation
- Internal Pivoting
- Port Forwarding
- Secure Administration

---

# Common Risks

- Weak Passwords
- Root Login Enabled
- Exposed Port 22
- Old SSH Versions
- Stolen Keys

---

# Useful Scan Commands

nmap -sV -p22 target-ip

hydra -l root -P rockyou.txt ssh://target-ip

(Use only in legal labs)

---

# Interview Questions

## What is SSH?

Secure remote access protocol.

## Default Port?

22

## Public vs Private Key?

Public key is shared.  
Private key is secret.

## What is authorized_keys?

Stores allowed public keys.

## What is ssh-agent?

Stores unlocked keys in memory.

---

# File Name

SSH.md

# Folder

01-Networking/SSH.md

# Author

Ketan Saini
Cyber Security Learning Repository
