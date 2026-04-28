# HTTP Status Codes & Cyber Kill Chain

## What are HTTP Status Codes?

HTTP Status Codes are standard responses sent by a web server to indicate the result of a client’s request.

They help identify whether the request was successful, redirected, invalid, or failed due to a server issue.

---

# HTTP Status Code Categories

## 100 - 199 : Informational Responses

These codes mean the server received part of the request and the client should continue sending the rest.

Used as a "continue processing" signal.

Examples:

- 100 Continue
- 101 Switching Protocols

---

## 200 - 299 : Success Responses

These codes mean the request was successful and processed correctly.

Examples:

- 200 OK
- 201 Created
- 204 No Content

---

## 300 - 399 : Redirection Responses

These codes indicate the requested resource has moved to another location.

Examples:

- 301 Moved Permanently
- 302 Found
- 304 Not Modified

---

## 400 - 499 : Client Error Responses

These codes indicate a problem in the request sent by the client.

Examples:

- 400 Bad Request
- 401 Unauthorized
- 403 Forbidden
- 404 Not Found
- 405 Method Not Allowed

---

## 500 - 599 : Server Error Responses

These codes indicate the server failed while processing a valid request.

Examples:

- 500 Internal Server Error
- 502 Bad Gateway
- 503 Service Unavailable
- 504 Gateway Timeout

---

# Important HTTP Status Codes

## 200 OK

The request completed successfully.

Example:

- Web page loaded correctly
- API request returned data

---

## 201 Created

A new resource was created successfully.

Example:

- New user account created
- Blog post added

---

## 301 Moved Permanently

The resource has permanently moved to a new URL.

Used for:

- SEO redirection
- Website migration

---

## 302 Found

Temporary redirect.

The resource is temporarily available at another location.

---

## 400 Bad Request

The request was invalid or missing required data.

Possible reasons:

- Invalid parameters
- Malformed syntax
- Missing fields

---

## 401 Unauthorized

Authentication is required.

You need to log in or provide credentials.

---

## 403 Forbidden

You are authenticated or unauthenticated, but access is denied.

Example:

- Admin page blocked

---

## 404 Not Found

The requested page or resource does not exist.

Most common web error.

---

## 405 Method Not Allowed

The HTTP method used is not allowed on that endpoint.

Example:

GET request sent where POST was required.

---

## 500 Internal Server Error

Generic server-side failure.

The server encountered an unexpected condition.

---

## 503 Service Unavailable

Server is overloaded or under maintenance.

Usually temporary.

---

# Common HTTP Methods

- GET = Retrieve data
- POST = Submit data
- PUT = Update data
- PATCH = Partial update
- DELETE = Remove data
- OPTIONS = Allowed methods
- HEAD = Headers only

---

# Cyber Security Importance of HTTP Codes

Used in:

- Web Pentesting
- API Testing
- Burp Suite
- Bug Bounty
- Reconnaissance
- Error Handling
- Enumeration

Examples:

- 200 = Resource exists
- 403 = Resource exists but blocked
- 404 = Resource not found
- 500 = Possible vulnerability / backend issue

---

# Useful Testing Examples

Check page:

GET /admin

Possible responses:

- 200 = Accessible
- 401 = Needs login
- 403 = Blocked
- 404 = Hidden / not found

---

# Cyber Kill Chain

Cyber Kill Chain is a model describing the stages of a cyber attack from planning to execution.

---

# 1. Reconnaissance

Collecting information about the target.

Examples:

- Finding IP addresses
- Subdomains
- Employee names
- Technologies used

Tools:

- Nmap
- Whois
- Google Dorking
- Subfinder

---

# 2. Weaponization

Preparing malicious payloads or attack tools.

Examples:

- Malware creation
- Exploit packaging
- Infected USB drives
- Macro documents

---

# 3. Delivery

Sending the payload to the target.

Examples:

- Phishing email
- USB device
- Malicious website
- Drive-by download

---

# 4. Exploitation

Triggering a vulnerability to gain access.

Examples:

- Buffer overflow
- SQL Injection
- RCE
- Browser exploit

---

# 5. Installation

Installing malware or backdoor for persistence.

Examples:

- RAT
- Trojan
- Keylogger
- Web shell

---

# 6. Command and Control (C2)

Attacker remotely controls the compromised machine.

Examples:

- Reverse shell
- Botnet communication
- Beaconing to server

---

# 7. Actions on Objectives

Attacker performs final goals.

Examples:

- Data theft
- Ransomware deployment
- Lateral movement
- Destroy systems
- Credential dumping

---

# Why Cyber Kill Chain Matters

Helps defenders detect and stop attacks early.

Best defense is stopping attacker before later stages.

---

# Interview Questions

## What does 404 mean?

Requested resource not found.

## Difference between 401 and 403?

401 = Authentication required  
403 = Access denied

## What does 500 indicate?

Internal server error.

## What is Reconnaissance?

Information gathering stage of an attack.

## What is C2?

Command and Control communication with attacker.

---

# Notes

- HTTP codes are critical in web testing.
- Cyber Kill Chain is important for SOC and Blue Team roles.
- Both topics are useful for interviews and pentesting.

---

# Author

Ketan Saini  
Cyber Security Learning Repository
