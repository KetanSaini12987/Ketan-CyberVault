# PASSWORD ENUMERATION

## What is Password Enumeration

Password enumeration is the process of discovering valid usernames, password reset weaknesses, login behavior differences, tokens, or hidden authentication flaws that help in gaining unauthorized access.

It usually happens when applications reveal too much information through:

- Error messages
- Password reset flows
- Tokens
- Different responses for valid vs invalid users
- Old archived files
- Brute-forceable OTP systems

> Use only in legal labs, CTFs, and authorized environments.

---

# 1. SQL Injection Based Enumeration

Sometimes login forms reveal database errors.

Example input:

```text id="mqep7m"
'
```

If backend is vulnerable, it may return SQL errors such as:

```text id="8n3d2j"
You have an error in your SQL syntax
```

This can reveal:

- Database type
- Query structure
- Table names
- Column names

---

## Common Test Inputs

```text id="c8rjlwm"
'
" 
' OR 1=1 --
admin' --
```

---

# 2. File Inclusion / Path Traversal Enumeration

Attackers manipulate file paths to discover internal files or system paths.

Example:

```text id="f1gjf3"
../../../../etc/passwd
```

or

```text id="0g53h9"
../../../../windows/win.ini
```

This may reveal:

- Usernames
- Installed services
- Internal folders
- Web root path

---

# 3. Weak Password Reset Token Enumeration

## Vulnerable PHP Example

```php id="n8z9u1"
$token = mt_rand(100, 200);
$query = $conn->prepare("UPDATE users SET reset_token = ? WHERE email = ?");
$query->bind_param("ss", $token, $email);
$query->execute();
```

## Why Vulnerable?

- Token range only from `100 to 200`
- Only 101 possible combinations
- Easy to brute-force

---

# 4. Generate OTP / Token Wordlist

Use `crunch` to generate all 3-digit values from 100 to 200.

```bash id="xw7w88"
crunch 3 3 -o otp.txt -t %%% -s 100 -e 200
```

## Meaning

| Option | Description |
|--------|-------------|
| 3 3 | Min and max length |
| -o | Output file |
| -t %%% | Numeric pattern |
| -s 100 | Start from 100 |
| -e 200 | End at 200 |

---

# 5. Basic Authentication Enumeration

Some websites use HTTP Basic Auth.

Format:

```http id="3f8t4y"
Authorization: Basic <credentials>
```

Where:

```text id="g7ph88"
<credentials> = base64(username:password)
```

Example:

```text id="0v1g62"
admin:password123
```

Convert to Base64:

```text id="aq4vvn"
YWRtaW46cGFzc3dvcmQxMjM=
```

Then send:

```http id="84g4km"
Authorization: Basic YWRtaW46cGFzc3dvcmQxMjM=
```

---

# 6. Username Enumeration via Responses

Sometimes apps return different messages:

```text id="v73quq"
Invalid username
```

vs

```text id="g4n3cm"
Wrong password
```

This means valid usernames can be discovered.

---

# 7. Timing Enumeration

Some login pages respond slower for real users because password hash verification occurs.

Example:

- Invalid user = fast response
- Valid user + wrong password = slower response

This can leak valid usernames.

---

# 8. Wayback Machine Enumeration

Older versions of websites may expose:

- Old admin panels
- Backup files
- Old APIs
- Hidden directories
- Old login portals

Website:

```text id="fnd7dw"
https://archive.org/web/
```

---

# 9. waybackurls Tool

Used to collect archived URLs.

## Installation

```bash id="p24y46"
git clone https://github.com/tomnomnom/waybackurls
cd waybackurls
sudo apt install golang-go -y
go build
ls -lah
```

## Usage

```bash id="fbh49f"
echo example.com | ./waybackurls
```

## Save Output

```bash id="5p3rrr"
echo example.com | ./waybackurls > urls.txt
```

---

# 10. Burp Suite for Enumeration

Use Burp Intruder / Repeater to test:

- OTP brute-force
- Username discovery
- Reset tokens
- Different responses
- Status codes
- Content length changes

---

# 11. Common Targets to Check

- `/login`
- `/admin`
- `/forgot-password`
- `/reset-password`
- `/api/login`
- `/backup.zip`
- `/old/`

---

# 12. Good Wordlists

```text id="5djlwm"
/usr/share/wordlists/rockyou.txt
/usr/share/seclists/Usernames/
/usr/share/seclists/Passwords/
```

---

# 13. Defensive Fixes

To prevent password enumeration:

- Use same error message for all failures
- Strong random reset tokens
- Rate limiting
- CAPTCHA
- MFA
- Lockout policy
- Logging and alerting

---

# Quick Commands Summary

```bash id="jvd3q7"
crunch 3 3 -o otp.txt -t %%% -s 100 -e 200
```

```bash id="jcvkh2"
echo example.com | ./waybackurls
```

```bash id="nqv0l2"
base64
```

---

# Notes

Password enumeration is often the first step before brute-force or account takeover. Even small leaks like different messages or weak reset tokens can become serious vulnerabilities.
