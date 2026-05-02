# SIEM 

## SIEM = Security Information and Event Management System

# 1) HOST-CENTRIC LOG SOURCES

These are log sources that capture events that occurred
within or related to the host.

Some log sources that generate host-centric logs are:
- Windows Event Logs
- Sysmon
- Osquery

Examples of Host-Centric Logs:
- A user accessing a file
- A user attempting to authenticate
- A process execution activity
- A process adding/editing/deleting a registry key or value
- PowerShell execution


# 2) NETWORK-CENTRIC LOG SOURCES

Network-related logs are generated when hosts communicate
with each other or access the internet.

Common Network Protocols:
- SSH
- VPN
- HTTP / HTTPS
- FTP

Examples of Network-Centric Events:
- SSH connection
- A file being accessed via FTP
- Web traffic
- A user accessing company resources through VPN
- Network file sharing activity


# WINDOWS MACHINE

Windows records every event that can be viewed through
the Event Viewer utility.

Each event is assigned a unique Event ID, which helps
security analysts track and investigate activities.

To open Event Viewer:

Event Viewer

Steps:
- Open Windows Search
- Type "Event Viewer"
- Open the utility


# LINUX WORKSTATION

Linux systems store logs related to:
- Events
- Errors
- Warnings
- Authentication
- Services

These logs are commonly ingested into a SIEM platform
for continuous monitoring.

Important Linux Log Locations:

/var/log/httpd

Contains:
- HTTP request logs
- HTTP response logs
- Error logs

/var/log/cron

Contains:
- Cron job related events

/var/log/auth.log
/var/log/secure

Contains:
- Authentication related logs

/var/log/kern

Contains:
- Kernel related events


# WEB SERVER

Monitoring web server logs is important to detect:
- Web attacks
- Unauthorized access
- Suspicious requests
- Server errors

Common Apache Log Locations in Linux:

/var/log/apache
/var/log/httpd

These directories commonly contain:
- Access logs
- Error logs
- Request / Response information


# QUICK SUMMARY

* Centralized Log Collection
* Security Monitoring
* Threat Detection
* Incident Investigation
* Event Correlation
* Real-Time Alerting
* Host Monitoring
* Network Monitoring
* Log Analysis
* Web Server Monitoring
