# SNORT

## Overview

Snort is an open-source **Network Intrusion Detection System (NIDS)** and **Intrusion Prevention System (IPS)**. It is used to monitor network traffic, detect attacks, generate alerts, and log packets.

---

## Rule Syntax

Snort rules are generally written in a single line.  
To continue a line, use `\`

### Basic Format

```bash
action protocol source_ip source_port -> destination_ip destination_port (rule options)
```

### Example Rule

```bash
alert tcp $HOME_NET any -> $EXTERNAL_NET $HTTP_PORTS (msg:"MALWARE-CNCWIN.Trojan.Tinba outbound connection"; flow:to_server,established; content:"/dataSafer3er/"; http_uri; content:"|8C 69 69 B2|"; http_client_body; classtype:trojan-activity; sid:1000000; rev:1;)
```

---

## Load Snort with Rules

```bash
sudo snort -c /etc/snort/snort.lua -R /etc/snort/rules/local.rules
```

| Option | Meaning |
|--------|---------|
| `-c` | Load configuration file |
| `-R` | Load custom rule file |

If `-R` is not used, only the Snort engine starts.

---

## Sniffer Mode

Used like Wireshark or tcpdump.

### Parameters

| Parameter | Description |
|----------|-------------|
| `-v` | Verbose output |
| `-d` | Show payload |
| `-e` | Show link-layer headers |
| `-X` | Full HEX packet dump |
| `-i` | Select interface |

### Commands

```bash
sudo snort -v -i eth0
```

```bash
snort -v
```

```bash
snort -d
```

```bash
snort -d -e
```

```bash
sudo snort -X
```

---

## Alert Mode

```bash
sudo snort -A console -q -c /etc/snort/snort.lua -i eth0 -R /etc/snort/rules/local.rules
```

| Option | Meaning |
|--------|---------|
| `-A console` | Show alerts in terminal |
| `-q` | Quiet mode |
| `-i eth0` | Use interface |

---

## Packet Logger Mode

Used to save packets into log files.

### Parameters

| Parameter | Description |
|----------|-------------|
| `-l` | Log directory |
| `-K ASCII` | Save logs in text format |
| `-r` | Read saved logs |
| `-n` | Limit packet count |
| `-V` | Show version |
| `-T` | Test config |
| `-q` | Quiet mode |

### Commands

```bash
sudo snort -dev -K ASCII -l /path/to/logdir
```

```bash
sudo snort -r snort.log.1638459842
```

```bash
sudo snort -r snort.log.1640048004 'tcp port 80'
```

---

## NIDS Mode

Detects suspicious traffic using rules.

### Parameters

| Parameter | Description |
|----------|-------------|
| `-c` | Config file |
| `-T` | Test configuration |
| `-N` | Disable logging |
| `-D` | Run in background |
| `-A` | Alert mode |

### Alert Modes

| Mode | Description |
|------|-------------|
| `full` | Full alert details |
| `fast` | Quick summary |
| `console` | Terminal alerts |
| `cmg` | Header + payload |
| `none` | Disable alerts |

### Example Rule

```bash
alert icmp any any <> any any (msg:"ICMP Packet Found"; sid:100001; rev:1;)
```

### Run in Background

```bash
sudo snort -c /etc/snort/snort.conf -D
```

### Check Process

```bash
ps -ef | grep snort
```

### Stop Process

```bash
sudo kill -9 2898
```

---

## PCAP Analysis Mode

Analyze saved `.pcap` packet captures.

### Parameters

| Parameter | Description |
|----------|-------------|
| `-r` | Read one pcap |
| `--pcap-list` | Read multiple pcaps |
| `--pcap-show` | Show filename during scan |

### Example

```bash
snort -c local.rules -A full -l . -r task9.pcap
```

---

## DAQ Configuration

DAQ = Data Acquisition Module

### Example

```bash
config daq: afpacket
config daq_mode: inline
config logdir: /var/log/snort
```

### DAQ Types

| Type | Purpose |
|------|---------|
| `pcap` | Default sniffing mode |
| `afpacket` | IPS inline mode |
| `ipq` | Linux Netfilter |
| `nfq` | Linux inline mode |
| `ipfw` | BSD firewall mode |
| `dump` | Testing mode |

---

## Useful Commands

```bash
snort -V
```

```bash
snort -T -c /etc/snort/snort.conf
```

```bash
sudo snort -q -A console -c /etc/snort/snort.conf -i eth0
```

---

## Summary

1. Sniffer Mode  
2. Logger Mode  
3. NIDS Detection Mode  
4. PCAP Analysis Mode  
5. IPS Inline Mode
