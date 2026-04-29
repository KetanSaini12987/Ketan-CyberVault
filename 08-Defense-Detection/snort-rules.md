#--------------------------------------------------#
SNORT RULES
#--------------------------------------------------#

ABOUT THIS FILE

This Snort configuration / rules file is used to configure:

- Network variables
- Detection engine
- Preprocessors
- Output logging
- Rule categories
- Custom rules

Compatible Version: Snort 2.9.7.0

#--------------------------------------------------#

STEP 1: NETWORK VARIABLES
```
ipvar HOME_NET any
ipvar EXTERNAL_NET any
```
Common Server Variables:
```
DNS_SERVERS  = $HOME_NET
SMTP_SERVERS = $HOME_NET
HTTP_SERVERS = $HOME_NET
SQL_SERVERS  = $HOME_NET
TELNET_SERVERS = $HOME_NET
SSH_SERVERS  = $HOME_NET
FTP_SERVERS  = $HOME_NET
SIP_SERVERS  = $HOME_NET
```
#--------------------------------------------------#

IMPORTANT PORT VARIABLES
```
HTTP_PORTS      = 80, 8080, 8000 etc
SSH_PORTS       = 22
FTP_PORTS       = 21, 2100, 3535
SIP_PORTS       = 5060, 5061
FILE_DATA_PORTS = HTTP + POP + IMAP
ORACLE_PORTS    = 1024:
SHELLCODE_PORTS = !80
```
#--------------------------------------------------#

PATH VARIABLES
```
RULE_PATH         = /etc/snort/rules
SO_RULE_PATH      = /etc/snort/so_rules
PREPROC_RULE_PATH = /etc/snort/preproc_rules
```
#--------------------------------------------------#

STEP 2: DECODER CONFIGURATION
```
config disable_decode_alerts
config disable_tcpopt_alerts
config disable_ipopt_alerts
config checksum_mode: all
```
#--------------------------------------------------#

STEP 3: DETECTION ENGINE
```
config pcre_match_limit: 3500
config pcre_match_limit_recursion: 1500
config detection: search-method ac-split
config event_queue: max_queue 8 log 5
```
#--------------------------------------------------#

STEP 4: DYNAMIC LIBRARIES
```
dynamicpreprocessor directory /usr/lib/snort_dynamicpreprocessor/
dynamicengine /usr/lib/snort_dynamicengine/libsf_engine.so
dynamicdetection directory /usr/lib/snort_dynamicrules
```
#--------------------------------------------------#

STEP 5: PREPROCESSORS
```
normalize_ip4
normalize_tcp
normalize_icmp4
normalize_ip6
normalize_icmp6
frag3
stream5
http_inspect
rpc_decode
ftp_telnet
smtp
ssh
dns
ssl
sip
imap
pop
modbus
dnp3
```
#--------------------------------------------------#

STEP 6: OUTPUT LOGGING
```
output unified2: filename snort.log, limit 128
```
#--------------------------------------------------#

STEP 7: ENABLED RULE FILES
```
attack-responses.rules
backdoor.rules
bad-traffic.rules
chat.rules
ddos.rules
dns.rules
dos.rules
exploit.rules
ftp.rules
icmp.rules
imap.rules
misc.rules
mysql.rules
oracle.rules
p2p.rules
policy.rules
pop3.rules
rpc.rules
scan.rules
smtp.rules
snmp.rules
sql.rules
telnet.rules
virus.rules
web-attacks.rules
web-cgi.rules
web-client.rules
web-iis.rules
web-misc.rules
web-php.rules
x11.rules

community-sql-injection.rules
community-web-client.rules
community-web-dos.rules
community-web-iis.rules
community-web-misc.rules
community-web-php.rules
```
#--------------------------------------------------#

STEP 8: PREPROCESSOR ALERT RULES
```
decoder.rules
preprocessor.rules
sensitive-data.rules
```
#--------------------------------------------------#

STEP 9: SHARED OBJECT RULES
```
bad-traffic.rules
chat.rules
dos.rules
exploit.rules
icmp.rules
imap.rules
misc.rules
multimedia.rules
netbios.rules
smtp.rules
snmp.rules
web-client.rules
web-iis.rules
```
#--------------------------------------------------#

LOCAL CUSTOM RULES
```
include $RULE_PATH/local.rules
```
Example:
```
alert icmp any any -> any any (msg:"ICMP Ping Detected"; sid:100001; rev:1;)
```
#--------------------------------------------------#

IMPORTANT COMMANDS
```
snort -T -c /etc/snort/snort.conf
snort -c /etc/snort/snort.conf -i eth0
snort -D -c /etc/snort/snort.conf
snort -r capture.pcap -c /etc/snort/snort.conf
```
Logs Folder:
```
/var/log/snort/
```
#--------------------------------------------------#

QUICK SUMMARY

✔ IDS (Intrusion Detection)
✔ IPS (Inline Prevention)
✔ Packet Sniffing
✔ Malware Detection
✔ SQLi Detection
✔ Port Scan Detection
✔ DDoS Detection
✔ Custom Rule Monitoring

#--------------------------------------------------#
