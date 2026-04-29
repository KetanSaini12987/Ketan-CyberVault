# NESSUS

## What is Nessus?
Nessus is a vulnerability assessment tool used to scan systems, networks, and web applications for security weaknesses.  
It helps identify misconfigurations, missing patches, and known vulnerabilities.

---

## Starting Nessus Service (Kali Linux)

### 1. Start Nessus Service

```
sudo systemctl start nessusd.service
```

---

### 2. Check Service Status

```
sudo systemctl status nessusd
```

- Ensures Nessus service is running properly

---

## Access Nessus Web Interface

1. Open browser and visit:

```
https://localhost:8834/
```

- Nessus runs on HTTPS port **8834**

---

## Nessus Setup Flow (First Time)

1. Open web interface
2. Create admin account
3. Enter activation code (from Tenable)
4. Download required plugins
5. Wait for plugin compilation

---

## Basic Usage Workflow

### 1. Create a New Scan
- Choose scan type:
  - Basic Network Scan
  - Advanced Scan
  - Web Application Scan

---

### 2. Target Input

```
192.168.1.1
```

or

```
192.168.1.0/24
```

or

```
example.com
```

---

### 3. Run Scan
- Click **Launch**
- Wait for vulnerability analysis

---

## Understanding Results

- **Critical** → Exploitable immediately
- **High** → Serious vulnerabilities
- **Medium** → Misconfigurations / weak points
- **Low** → Informational issues

---

## Important Nessus Features

### 1. Plugin System
- Uses vulnerability plugins
- Each plugin checks specific CVEs

---

### 2. Report Generation

```
HTML / PDF / CSV
```

- Used for documentation and reporting

---

### 3. Export Report
- Useful for:
  - Penetration testing reports
  - Compliance audits

---

## Useful Linux Commands (Related to Nessus)

### Restart Nessus

```
sudo systemctl restart nessusd.service
```

---

### Stop Nessus

```
sudo systemctl stop nessusd.service
```

---

### Enable Nessus on Boot

```
sudo systemctl enable nessusd.service
```

---

## Nessus Default Port

```
8834
```

- Always accessed via HTTPS:
```
https://localhost:8834
```

---

## Notes
- Nessus requires high system resources during scans
- Plugin updates must be kept current for accurate results
- Always scan authorized systems only
