# 🔐 PortSwigger Web Security Academy — Lab Write-ups

> **Kushal Nayaka** · Aspiring Penetration Tester & VAPT Analyst  
> Solving hands-on web security labs using **Burp Suite** with documented methodology, payloads, and remediation notes.

[![Labs Solved](https://img.shields.io/badge/Labs%20Solved-35%2B-brightgreen?style=flat-square)](https://github.com/kushalanayaka/portswigger-labs)
[![Platform](https://img.shields.io/badge/Platform-PortSwigger%20Web%20Security%20Academy-orange?style=flat-square)](https://portswigger.net/web-security)
[![Tool](https://img.shields.io/badge/Tool-Burp%20Suite-red?style=flat-square)](https://portswigger.net/burp)
[![OWASP](https://img.shields.io/badge/Standard-OWASP%20Top%2010-blue?style=flat-square)](https://owasp.org/www-project-top-ten/)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-kushalnayaka-0077B5?style=flat-square&logo=linkedin)](https://www.linkedin.com/in/kushalnayaka)

---

## 📌 About This Repository

This repository documents my hands-on practice with web application security through PortSwigger Web Security Academy labs. Every lab includes:

- ✅ **Objective** — what vulnerability is being exploited
- ✅ **Attack methodology** — step-by-step approach
- ✅ **Payloads used** — exact inputs and techniques
- ✅ **Burp Suite usage** — tools and features applied (Repeater, Intruder, Decoder, etc.)
- ✅ **Remediation** — how the vulnerability should be fixed in real applications

> 🎯 Goal: Build a verifiable, public skill record demonstrating practical offensive security knowledge aligned with **OWASP Top 10**.

---

## 🗂️ Lab Categories

| # | Category | Labs Completed | Key Techniques |
|---|----------|----------------|----------------|
| 1 | [SQL Injection](#-sql-injection) | ✅ | UNION attacks, Blind SQLi, Error-based |
| 2 | [Cross-Site Scripting (XSS)](#-cross-site-scripting-xss) | ✅ | Reflected, Stored, DOM-based XSS |
| 3 | [CSRF](#-csrf---cross-site-request-forgery) | ⌛ | Token bypass, SameSite exploitation |
| 4 | [SSRF](#-ssrf---server-side-request-forgery) | ⌛ | Internal service access, cloud metadata |
| 5 | [Authentication](#-authentication) | ⌛ | Brute force, MFA bypass, password reset flaws |
| 6 | [Access Control](#-access-control) | ⌛ | IDOR, privilege escalation, URL-based bypass |

---

## 🛡️ SQL Injection

**Vulnerability:** Attacker-controlled input is interpreted as SQL commands, allowing unauthorized data access, authentication bypass, or database manipulation.

**OWASP Category:** A03:2021 — Injection

**Labs covered:**
- SQL injection UNION attack — determining number of columns
- SQL injection UNION attack — finding columns with text data
- SQL injection UNION attack — retrieving data from other tables
- SQL injection with filter bypass via XML encoding
- Blind SQL injection with conditional responses
- Blind SQL injection with time delays

**Key tools:** Burp Suite Repeater, Intruder

**Sample payload approach:**
```sql
' UNION SELECT NULL,NULL,NULL--
' OR 1=1--
'; SELECT pg_sleep(5)--
```

**Remediation:** Use parameterized queries / prepared statements. Never concatenate user input into SQL strings.

📁 [View SQL Injection Write-ups →](./SQL-Injection/)

---

## 🔥 Cross-Site Scripting (XSS)

**Vulnerability:** Malicious scripts are injected into web pages viewed by other users, enabling session hijacking, credential theft, or defacement.

**OWASP Category:** A03:2021 — Injection

**Labs covered:**
- Reflected XSS into HTML context with nothing encoded
- Stored XSS into HTML context with nothing encoded
- DOM XSS in `document.write` sink using `location.search`
- DOM XSS in jQuery anchor `href` attribute sink
- Reflected XSS into attribute with angle brackets HTML-encoded
- XSS context with most tags and attributes blocked (WAF bypass)

**Key tools:** Burp Suite Repeater, browser DevTools

**Sample payload approach:**
```html
<script>alert(1)</script>
<img src=x onerror=alert(document.cookie)>
javascript:alert(document.domain)
```

**Remediation:** Encode output contextually (HTML, JS, URL). Use Content Security Policy (CSP). Avoid `innerHTML` and `eval()`.

📁 [View XSS Write-ups →](./XSS/)

---

## 🔄 CSRF — Cross-Site Request Forgery

**Vulnerability:** A malicious site tricks an authenticated user's browser into making unintended requests to another site, performing actions on their behalf.

**OWASP Category:** A01:2021 — Broken Access Control

**Labs covered:**
- CSRF vulnerability with no defenses
- CSRF where token validation depends on request method
- CSRF where token is not tied to user session
- CSRF where Referer validation depends on header being present
- SameSite Lax bypass via method override

**Key tools:** Burp Suite CSRF PoC Generator, Repeater

**Remediation:** Implement CSRF tokens tied to user session. Use `SameSite=Strict` cookies. Validate `Origin` and `Referer` headers.

📁 [View CSRF Write-ups →](./CSRF/)

---

## 🌐 SSRF — Server-Side Request Forgery

**Vulnerability:** An attacker causes the server to make HTTP requests to unintended locations — internal services, cloud metadata endpoints, or other back-end systems.

**OWASP Category:** A10:2021 — Server-Side Request Forgery

**Labs covered:**
- Basic SSRF against the local server
- Basic SSRF against another back-end system
- SSRF with blacklist-based input filter bypass
- SSRF with filter bypass via open redirection
- Blind SSRF with out-of-band detection

**Key tools:** Burp Suite Repeater, Collaborator (OOB detection)

**Sample payload approach:**
```
http://localhost/admin
http://192.168.0.1/admin
http://169.254.169.254/latest/meta-data/  (AWS metadata)
```

**Remediation:** Whitelist allowed destinations. Disable unnecessary URL schemes. Block internal IP ranges server-side.

📁 [View SSRF Write-ups →](./SSRF/)

---

## 🔑 Authentication

**Vulnerability:** Weaknesses in login mechanisms allow attackers to gain unauthorized access through brute force, credential stuffing, or logic flaws in password reset flows.

**OWASP Category:** A07:2021 — Identification and Authentication Failures

**Labs covered:**
- Username enumeration via different responses
- Username enumeration via subtly different responses
- Username enumeration via response timing
- Broken brute-force protection — IP block bypass
- 2FA simple bypass
- Password reset broken logic
- Brute-forcing a stay-logged-in cookie

**Key tools:** Burp Suite Intruder, Decoder

**Remediation:** Implement account lockout, rate limiting, and generic error messages. Validate 2FA tokens server-side. Use secure, random password reset tokens with short expiry.

📁 [View Authentication Write-ups →](./Authentication/)

---

## 🚪 Access Control

**Vulnerability:** Users can access resources or perform actions beyond their intended permissions — vertically (admin functions) or horizontally (other users' data).

**OWASP Category:** A01:2021 — Broken Access Control

**Labs covered:**
- Unprotected admin functionality
- User role controlled by request parameter
- User ID controlled by request parameter (IDOR)
- Insecure direct object references (IDOR) — accessing other users' files
- URL-based access control that can be circumvented
- Multi-step process with no access control on one step
- Referer-based access control

**Key tools:** Burp Suite Repeater, browser DevTools

**Sample IDOR approach:**
```
GET /my-account?id=1   →   change to id=2
GET /download?file=user1.txt   →   change to user2.txt
```

**Remediation:** Enforce server-side access control checks on every request. Never rely on hidden fields or client-side enforcement. Implement least-privilege principles.

📁 [View Access Control Write-ups →](./Access-Control/)

---

## 🛠️ Tools & Environment

| Tool | Purpose |
|------|---------|
| **Burp Suite Community** | Intercepting proxy, Repeater, Intruder, Decoder |
| **Browser DevTools** | DOM analysis, JS debugging, network inspection |
| **PortSwigger Academy** | Lab environment |
| **Python** | Custom scripts for automation and payload generation |

---

## 📈 Progress Tracker

```
SQL Injection      ████████████████████  ✅ Complete
XSS                ████████████████████  ✅ Complete
CSRF                ░░░░░░░░░░░░░░░░░░░  ⌛ In Progress
SSRF               ░░░░░░░░░░░░░░░░░░░░  🔄 In Progress
Authentication     ░░░░░░░░░░░░░░░░░░░░  🔄 In Progress
Access Control     ░░░░░░░░░░░░░░░░░░░░  🔄 In Progress
Business Logic     ░░░░░░░░░░░░░░░░░░░░  🔄 In Progress
OS Command Inj.    ░░░░░░░░░░░░░░░░░░░░  🔄 Upcoming
File Upload Vulns  ░░░░░░░░░░░░░░░░░░░░  🔄 Upcoming
JWT Attacks        ░░░░░░░░░░░░░░░░░░░░  🔄 Upcoming
```

---

## 📚 Learning Resources

- 🔗 [PortSwigger Web Security Academy](https://portswigger.net/web-security) — Free, hands-on labs
- 🔗 [OWASP Top 10 (2021)](https://owasp.org/www-project-top-ten/) — Industry-standard vulnerability classification
- 🔗 [Burp Suite Documentation](https://portswigger.net/burp/documentation) — Tool reference
- 🔗 [OWASP Testing Guide](https://owasp.org/www-project-web-security-testing-guide/) — Professional pentest methodology

---

## 🙋 About Me

**Kushal Nayaka** — Computer Science graduate and aspiring cybersecurity professional based in Bangalore.

Currently interning at **STQC (Standardisation Testing and Quality Certification)** under MeitY, Government of India, and actively building hands-on offensive security skills through daily lab practice.

- 💼 **Open to:** Junior Penetration Tester · VAPT Analyst · SOC Analyst
- 📧 **Email:** kushal.cbv@gmail.com
- 🔗 **LinkedIn:** [linkedin.com/in/kushalnayaka](https://www.linkedin.com/in/kushalnayaka)
- 🐙 **GitHub:** [github.com/kushalanayaka](https://github.com/kushalanayaka)

---

> *"Security is not a product, but a process."* — Bruce Schneier

⭐ If this repo helped you learn something, consider starring it!
