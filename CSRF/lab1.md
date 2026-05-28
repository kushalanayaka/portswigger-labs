# 🔐 Lab 1: CSRF Vulnerability with No Defenses

## 🧩 Objective
To exploit a Cross-Site Request Forgery (CSRF) vulnerability caused by the absence of anti-CSRF protections.

## 🔍 Vulnerability
The application performs sensitive actions based solely on the user's authenticated session without verifying whether the request was intentionally initiated by the legitimate user.

Because no CSRF defenses are implemented, an attacker can craft a malicious request that executes actions on behalf of the victim.

## ⚙️ Exploit Used

```html
<form action="https://YOUR-LAB-ID.web-security-academy.net/my-account/change-email" method="POST">
    <input type="hidden" name="email" value="attacker@evil.com">
</form>

<script>
    document.forms[0].submit();
</script>
```

## 🔎 Context
- **Vulnerability Type:** Cross-Site Request Forgery (CSRF)  
- **Affected Functionality:** Change email feature  
- **Protection Present:** None  

## 🔎 Analysis
1. The victim is authenticated to the application  
2. The application accepts state-changing POST requests without CSRF validation  
3. The attacker creates a malicious HTML page containing a forged request  
4. When the victim visits the malicious page, the browser automatically submits the request  
5. The victim’s email address is changed without their consent  

## 💡 Exploit Explanation

- `<form>` → creates a forged request targeting the vulnerable endpoint  
- `method="POST"` → matches the legitimate request method  
- `input type="hidden"` → silently supplies attacker-controlled data  
- `document.forms[0].submit()` → automatically submits the form when the page loads  

### 👉 How it works
- Browsers automatically include the victim’s session cookies with requests  
- Since the application does not verify request origin or CSRF tokens, the request is trusted  
- The action is performed using the victim’s authenticated session  

### 👉 Why this exploit works
- No anti-CSRF token validation  
- No SameSite cookie protection  
- No Origin or Referer verification  

## 🚀 Steps to Reproduce
1. Log into the victim account  
2. Intercept the email change request using Burp Suite  
3. Generate a CSRF proof-of-concept (PoC) HTML page  
4. Modify the email parameter to an attacker-controlled value  
5. Host or open the exploit page in the victim’s browser  
6. Observe automatic form submission  
7. Verify that the email address changes successfully  

## ✅ Result
The victim’s email address is changed without their knowledge or consent, confirming the CSRF vulnerability.

## 🧠 Key Learning
Applications must verify whether sensitive requests originate from legitimate user actions. Without CSRF protection, attackers can abuse authenticated sessions to perform unauthorized actions.

## 🛡️ Prevention
- Implement anti-CSRF tokens  
- Use SameSite cookies  
- Validate Origin and Referer headers  
- Require password re-authentication for sensitive actions  

---

## 📸 Screenshots

<img width="1258" height="599" alt="image" src="https://github.com/user-attachments/assets/edc13775-fac2-42b0-b94d-b387e67f4e80" />

**Figure 1: Original User name and Email address**

<br>

<img src="ADD_YOUR_IMAGE_LINK_2" />

**Figure 2: Generated CSRF proof-of-concept exploit**

<br>

<img src="ADD_YOUR_IMAGE_LINK_3" />

**Figure 3: Successful email change via CSRF attack (Lab Solved)**
