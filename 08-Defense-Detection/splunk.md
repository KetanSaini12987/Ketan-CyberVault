#--------------------------------------------------#
SPLUNK
#--------------------------------------------------#

ABOUT SPLUNK

Splunk is a SIEM / log analysis platform used for:

- Log Collection
- Monitoring
- Threat Detection
- Dashboards
- Alerts
- Incident Investigation
- Searching Large Data Sources

#--------------------------------------------------#

INSTALLING SPLUNK

Download Splunk:
```
wget -O splunk.tgz "https://download.splunk.com/products/splunk/releases/9.0.3/linux/splunk-9.0.3-dd0128b1f8cd-Linux-x86_64.tgz"
```
Extract File:
```
tar -xvzf splunk.tgz
```
This creates extracted folder:
```
splunk/
```
#--------------------------------------------------#

START SPLUNK

Move into folder:
```
cd splunk
```
First Time Start:
```
./bin/splunk start --accept-license
```
Used for:

- Accept license
- Create username/password
- Start Splunk service

Default URL:
```
http://127.0.0.1:8000
```
#--------------------------------------------------#

CHECK STATUS
```
sudo ./bin/splunk status
```
#--------------------------------------------------#

START AFTER ACCOUNT CREATED
```
sudo ./bin/splunk start --accept-license --answer-yes
```
#--------------------------------------------------#

STOP SPLUNK
```
sudo ./bin/splunk stop
```
#--------------------------------------------------#

SEARCH BAR COMMANDS

SHOW ALL INGESTED LOGS
```
index=main
```
(Select All Time to see full logs)

#--------------------------------------------------#

SHOW WEB TRAFFIC LOGS
```
index=main sourcetype=web_traffic
```
#--------------------------------------------------#

EVENT COUNT PER DAY
```
index=main sourcetype=web_traffic | timechart span=1d count
```
#--------------------------------------------------#

SORT DAILY COUNT DESCENDING
```
index=main sourcetype=web_traffic | timechart span=1d count | sort -count
```
#--------------------------------------------------#

REMOVE NORMAL BROWSERS / FIND SUSPICIOUS AGENTS
```
index=main sourcetype=web_traffic user_agent!=*Mozilla* user_agent!=*Chrome* user_agent!=*Safari* user_agent!=*Firefox*
```
#--------------------------------------------------#

TOP 5 SUSPICIOUS IPS
```
sourcetype=web_traffic user_agent!=*Mozilla* user_agent!=*Chrome* user_agent!=*Safari* user_agent!=*Firefox* | stats count by client_ip | sort -count | head 5
```
#--------------------------------------------------#

PROBING EXPOSED FILES
```
sourcetype=web_traffic client_ip="Suspicious_IP" AND path IN ("/.env","/*phpinfo*","/.git*") | table _time path user_agent status
```
#--------------------------------------------------#

PATH TRAVERSAL / OPEN REDIRECT
```
sourcetype=web_traffic client_ip="Suspicious_IP" AND path="*..*" OR path="*redirect*"
```
#--------------------------------------------------#

COUNT TRAVERSAL ATTEMPTS
```
sourcetype=web_traffic client_ip="Suspicious_IP" AND path="*..\/..\/*" OR path="*redirect*" | stats count by path
```
#--------------------------------------------------#

SQLMAP / HAVIJ DETECTION
```
sourcetype=web_traffic client_ip="Suspicious_IP" AND user_agent IN ("*sqlmap*","*Havij*") | table _time path status
```
#--------------------------------------------------#

BACKUP / LOG FILE DOWNLOAD ATTEMPTS
```
sourcetype=web_traffic client_ip="Suspicious_IP" AND path IN ("*backup.zip*","*logs.tar.gz*") | table _time path user_agent
```
#--------------------------------------------------#

FIREWALL ALLOWED TRAFFIC TO ATTACKER
```
sourcetype=firewall_logs src_ip="10.10.1.5" AND dest_ip="Suspicious_IP" AND action="ALLOWED" | table _time action protocol src_ip dest_ip dest_port reason
```
#--------------------------------------------------#

TOTAL DATA EXFILTRATION
```
sourcetype=firewall_logs src_ip="10.10.1.5" AND dest_ip="Suspicious_IP" AND action="ALLOWED" | stats sum(bytes_transferred) by src_ip
```
#--------------------------------------------------#

IMPORTANT COMMANDS SUMMARY
```
./bin/splunk start --accept-license
./bin/splunk status
./bin/splunk stop
```
#--------------------------------------------------#

## QUICK SUMMARY

* SIEM Tool
* Log Monitoring
* Web Log Analysis
* Firewall Analysis
* Threat Hunting
* Dashboarding
* Incident Response
* IOC Search

#--------------------------------------------------#
