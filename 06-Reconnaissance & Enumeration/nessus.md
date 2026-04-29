# NESSUS

## What is Nessus
Nessus is a vulnerability scanner used to detect security weaknesses in systems, networks, and applications. It is similar to Nmap but focuses on vulnerability assessment.

---

## Starting Nessus Service

### Start Nessus
```bash
sudo systemctl start nessusd.service
```

### Check Status
```bash
sudo systemctl status nessusd
```

### Enable on Boot (Optional)
```bash
sudo systemctl enable nessusd.service
```

---

## Access Nessus Web Interface

Open in browser:
```text
https://localhost:8834/
```

If remote system:
```text
https://<target-ip>:8834/
```

---

## Nessus Setup Steps

1. Open browser and visit:
```text
https://localhost:8834/
```

2. Create account:
- Admin username
- Password

3. Choose edition:
- Nessus Essentials (free)
- Nessus Professional (paid)

4. Activate with activation code (Essentials key required)

5. Wait for plugin download and initialization

---

## Basic Nessus Workflow

### 1. Create New Scan
- Click "New Scan"
- Choose scan type:
  - Basic Network Scan
  - Advanced Scan
  - Web Application Scan

---

### 2. Configure Scan

Example settings:
```text
Name: Test Scan
Target: 192.168.1.10
```

---

### 3. Launch Scan
- Click "Save"
- Click "Launch"

---

### 4. View Results
- Critical vulnerabilities (High risk)
- Medium vulnerabilities
- Low informational issues

---

## Nessus Scan Types

| Scan Type | Description |
|----------|-------------|
| Basic Network Scan | General vulnerability scan |
| Advanced Scan | Custom scan with full control |
| Web Application Scan | Web-based vulnerability testing |
| Malware Scan | Detects malicious files |
| Compliance Scan | Checks system policy compliance |

---

## Important Nessus Features

### Plugin System
- Nessus uses plugins to detect vulnerabilities
- Plugins are updated regularly

---

### Report Export
```text
HTML → Easy viewing
PDF → Documentation
CSV → Data analysis
```

---

## Common Use Cases

- Finding outdated software
- Detecting open vulnerable ports
- Checking misconfigurations
- Identifying CVEs
- Compliance auditing

---

## Example Attack Flow (Ethical Testing)

1. Scan target using Nessus
2. Identify vulnerabilities
3. Cross-check with Nmap
4. Verify exploitability manually
5. Report findings

---

## Extra Useful Commands (Linux support check)

Check if Nessus is running:
```bash
ps aux | grep nessus
```

Restart service:
```bash
sudo systemctl restart nessusd.service
```

Stop service:
```bash
sudo systemctl stop nessusd.service
```

---

## Notes
- Nessus runs on port `8834`
- Always use in authorized environments only
- Best used with Nmap for full recon + vuln assessment combo
