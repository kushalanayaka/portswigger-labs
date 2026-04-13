# 🔐 Lab 19: Reflected XSS into a JavaScript String with Angle Brackets and Double Quotes HTML-Encoded and Single Quotes Escaped

## 🧩 Objective
To exploit a vulnerability in a JavaScript string where multiple encoding protections are applied.

## 🔍 Vulnerability
The application attempts to secure user input by:
- HTML-encoding angle brackets and double quotes  
- Escaping single quotes  
However, improper handling of escape characters allows breaking out of the JavaScript string.

## ⚙️ Payload Used
`\';alert(1)//`

## 🔎 Context
- **Source:** User input (URL parameter)  
- **Sink:** JavaScript string inside `<script>`  
- **Type:** Reflected XSS (JS escape bypass)  

## 🔎 Analysis
1. User input is inserted inside a JavaScript string  
2. Single quotes are escaped using backslash  
3. Attacker injects a backslash to neutralize escaping  
4. The string is terminated  
5. JavaScript code is injected and executed  
6. Remaining code is commented out  

## 💡 Payload Explanation
- `\` → escapes the escape character  
- `'` → closes the JavaScript string  
- `;` → terminates the statement  
- `alert(1)` → executes JavaScript  
- `//` → comments out remaining code  

👉 How it works:
- The application escapes `'` as `\'`  
- Injecting `\` cancels the escaping behavior  
- This allows breaking out of the string  
- JavaScript executes successfully  

👉 Why this payload works:
- Escaping is not handled safely  
- Backslash manipulation breaks protection  
- The application does not validate JS context properly  

## 🚀 Steps to Reproduce
1. Navigate to the vulnerable page  
2. Modify the URL parameter:  
   `?search=\';alert(1)//`
3. Press Enter  
4. Observe JavaScript execution  

## ✅ Result
JavaScript alert is triggered, confirming successful XSS via escape bypass.

## 🧠 Key Learning
Escaping characters is not sufficient if attackers can manipulate escape sequences. Proper context-aware encoding is required.

## 🛡️ Prevention
- Use strict JavaScript encoding (e.g., JSON encoding)  
- Avoid embedding user input directly in scripts  
- Use secure templating frameworks  
- Implement Content Security Policy (CSP)  

---

## 📸 Screenshots

<img width="1364" height="678" alt="LAB19_1" src="https://github.com/user-attachments/assets/f451bf7a-a372-451d-a47e-878c28cb6c45" />

**Figure 1: Injecting payload into URL parameter, Payload breaking JavaScript string via escape bypass and JavaScript execution (Lab Solved)**

