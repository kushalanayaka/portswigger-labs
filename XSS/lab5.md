# 🔐 Lab 5: DOM XSS in jQuery anchor href attribute sink using location.search

## 🧩 Objective
To exploit a where user input is used to set the href attribute of an anchor tag using jQuery.

## 🔍 Vulnerability
The application reads user input from location.search and assigns it directly to the href attribute of an anchor element using jQuery without validation, allowing JavaScript execution.

## ⚙️ Payload Used
javascript:alert(1)

## 🔎 Analysis
1. The application reads input from location.search  
2. jQuery assigns this value to an anchor tag's href attribute  
3. No validation or sanitization is applied  
4. Attacker injects javascript: scheme  
5. JavaScript executes when the link is clicked  

## 🚀 Steps to Reproduce
1. Navigate to the vulnerable page  
2. Modify the URL parameter:  
   ?returnUrl=javascript:alert(1)  
3. Press Enter  
4. Click the generated link  
5. Observe JavaScript execution  

## ✅ Result
JavaScript alert is triggered when the link is clicked, confirming DOM-based XSS.

## 🧠 Key Learning
DOM XSS can occur when untrusted input is used to dynamically set attributes like href, especially with dangerous schemes like javascript:.

## 🛡️ Prevention
- Validate and restrict allowed URL schemes (e.g., only http/https)  
- Avoid assigning user input directly to href attributes  
- Sanitize input before using in DOM  
- Use safe APIs and Content Security Policy (CSP)  

---

## 📸 Screenshots


<img width="1360" height="641" alt="LAB5_1" src="https://github.com/user-attachments/assets/24d40a68-fc21-4277-8010-63ed803da368" />
<br><br>
**Figure 1: JavaScript execution after clicking the link (Lab Solved)**
