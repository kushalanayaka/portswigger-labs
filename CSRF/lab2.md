# 🔐 Lab 2: CSRF Where Token Validation Depends on Request Method

## 🧩 Objective
To exploit a CSRF vulnerability where the application validates the CSRF token only for specific HTTP request methods.

## 🔍 Vulnerability
The application enforces CSRF token validation for `POST` requests but fails to validate tokens for `GET` requests.

An attacker can bypass CSRF protection by changing the request method from `POST` to `GET`.

## ⚙️ Exploit Used

```html
<img src="https://YOUR-LAB-ID.web-security-academy.net/my-account/change-email?email=attacker@evil.com">
```

## 🔎 Context
- **Vulnerability Type:** Cross-Site Request Forgery (CSRF)  
- **Affected Functionality:** Change email feature  
- **Protection Present:** CSRF token validation only for POST requests  

## 🔎 Analysis
1. The application normally changes email using a `POST` request  
2. CSRF token validation is enforced only for `POST` requests  
3. The endpoint also accepts `GET` requests  
4. The attacker changes the request method from `POST` to `GET`  
5. The forged request executes without requiring a CSRF token  

## 💡 Exploit Explanation

- `<img>` → automatically sends a GET request when loaded by the browser  
- `src=` → points to the vulnerable endpoint  
- `email=attacker@evil.com` → attacker-controlled parameter  

### 👉 How it works
- Browsers automatically request resources referenced in the `src` attribute  
- The victim’s session cookies are included automatically  
- Since the application skips CSRF validation for GET requests, the request succeeds  

### 👉 Why this exploit works
- CSRF validation depends only on request method  
- Sensitive functionality incorrectly accepts GET requests  
- No validation is performed for state-changing GET requests  

## 🚀 Steps to Reproduce
1. Log into the victim account  
2. Intercept the legitimate email change request using Burp Suite  
3. Observe that the request uses the POST method with CSRF token validation  
4. Change the request method from POST to GET  
5. Remove the CSRF token parameter  
6. Verify that the request still succeeds  
7. Create a malicious HTML page using the payload above  
8. Open the exploit page while authenticated  
9. Observe the email address changing successfully  

## ✅ Result
The victim’s email address is changed without a valid CSRF token by abusing a GET request, confirming the vulnerability.

## 🧠 Key Learning
CSRF protection must be enforced consistently across all HTTP methods. Sensitive actions should never be performed through GET requests.

## 🛡️ Prevention
- Enforce CSRF validation for all state-changing requests  
- Do not allow sensitive actions through GET requests  
- Use SameSite cookies  
- Validate Origin and Referer headers  

---

## 📸 Screenshots

<img src="ADD_YOUR_IMAGE_LINK_1" />

**Figure 1: Legitimate POST request with CSRF token**

<br>

<img src="ADD_YOUR_IMAGE_LINK_2" />

**Figure 2: Modified GET request without CSRF token**

<br>

<img src="ADD_YOUR_IMAGE_LINK_3" />

**Figure 3: Successful CSRF attack using GET request (Lab Solved)**
