# WINDOWS PRIVILEGE ESCALATION / WINDOWS ROOM

# REMOTE ACCESS (RDP)
```
xfreerdp3 /u:administrator /p:letmein123! /v:10.10.86.110
```
→ /u is username
→ /p is password
→ /v is target IP address
→ Opens Windows Remote Desktop session

rdesktop -u sg <host_IP>
→ Connects to Windows RDP server using username "sg"


# WINDOWS GUI / SYSTEM TOOLS (RUN COMMANDS)

win + R → lusrmgr.msc
→ Opens Local Users and Groups (user management interface)

msconfig
→ System Configuration (boot, services, startup, users)

taskmgr
→ Opens Task Manager

winver.exe
→ Shows Windows version information

compmgmt
→ Opens Computer Management console

perfmon
→ Opens Performance Monitor

msinfo32
→ Shows full system information (hardware + OS details)

resmon
→ Opens Resource Monitor (CPU, RAM, disk, network usage)

regedit
→ Opens Windows Registry Editor

wf.msc
→ Opens Windows Firewall settings


# COMMAND LINE ENUMERATION

net users
→ Lists all user accounts on the system

net user <username>
→ Shows detailed information of a specific user

ipconfig /?
→ Displays help for ipconfig command


# USER MANAGEMENT (PRACTICAL ADMIN ACTIONS)

net user <username> /add
→ Creates a new user in Windows

Event ID 4720
→ Logs user creation events in Event Viewer


# REGISTRY AND SYSTEM ENUMERATION

reg query "HKEY_LOCAL_MACHINE\Software\Microsoft\Internet Explorer" /v svcVersion
→ Retrieves Internet Explorer version from registry
→ Useful for system fingerprinting


# TASK SCHEDULING (PERSISTENCE TECHNIQUE)

schtasks /create /tn "T1053_005_OnLogon" /sc onlogon /tr "cmd.exe /c calc.exe"
→ Creates a scheduled task that runs on user login
→ Used for persistence and execution tracking


# RECON AND SECURITY TOOLS

sudo wig http://<IP>
→ Web Application Information Gatherer (WIG)
→ Used for web fingerprinting and reconnaissance


# WINDOWS FORENSICS / LOG TRACKING NOTES

Event Viewer is used to track:
- User creation (Event ID 4720)
- Registry changes
- Scheduled task execution
- System activity via Sysmon logs
