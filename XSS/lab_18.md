# 🔐 Lab 18: Reflected XSS into a JavaScript String with Single Quote and Backslash Escaped

## 🧩 Objective
To exploit a XSS vulnerability where user input is embedded inside the javascript string quotes and backslashes escaped

## 🔍 Vulnerability
The application attemppts to prevent XSS by escaping single quotes and blacklashes, But it fails to prevent breaking out of the `<script>` context.

## ⚙️ Payload Used
`</script><script>alert(1)</script>`

## 🔎 Context
- **Source:** User input (URL parameter)  
- **Sink:** JavaScript string inside `<script>` tag  
- **Type:** Reflected XSS (script context bypass)  

## 🔎 Analysis
1. User input is placed inside a Javascript string
2. Single qoute and backlashes are escaped
3. Direct string breaking is not possible
4. Attacker injects `</script>` to close the script block
5. A new `<script>` tag is injected
6. Javascript execution in the new script block 

## 💡 Payload Explanation
- `</script>` → closes the existing script tag  
- `<script>` → opens a new script block  
- `alert(1)` → executes JavaScript  

👉 How it works:
- The browser parses HTML before JavaScript  
- Closing the `<script>` tag ends the current script  
- A new script tag is injected and executed  

👉 Why this payload works:
- Escaping applies only inside JavaScript string  
- HTML parsing is separate from JavaScript parsing  
- The application does not sanitize HTML context properly  

## 🚀 Steps to Reproduce
1. Navigate to the vulnerable page  
2. Modify the URL parameter:  
   `?search=</script><script>alert(1)</script>`
3. Press Enter  
4. Observe JavaScript execution  

## ✅ Result
JavaScript alert is triggered, confirming successful XSS via script context escape.

## 🧠 Key Learning
Escaping characters inside JavaScript strings is not sufficient if attackers can break out of the `<script>` tag itself.

## 🛡️ Prevention
- Encode output for both HTML and JavaScript contexts  
- Avoid embedding user input directly in script blocks  
- Use safe APIs (e.g., JSON encoding)  
- Implement Content Security Policy (CSP)  

---

## 📸 Screenshots

<img width="1359" height="683" alt="LAB18_1" src="https://github.com/user-attachments/assets/125d2bd2-be1e-4236-a40a-f624df3949e9" />

**Figure 1: Injecting payload into URL parameter using Burp Suite Repeater**

<br>

<img width="1358" height="666" alt="LAB18_2" src="https://github.com/user-attachments/assets/d2ae941a-831b-4dc1-b250-89881277283c" />

**Figure 2: JavaScript execution via injected script (Lab Solved)**

