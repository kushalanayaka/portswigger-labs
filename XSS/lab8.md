# 🔐 Lab 8: Stored XSS into Anchor href Attribute with Double Quotes HTML-Encoded

## 🧩 Objective
To exploit a stored XSS vulnerability where user input is embedded inside an anchor href attribute with quotes encoded.

## 🔍 Vulnerability
Although double quotes are encoded, the application does not validate URL schemes, allowing javascripts execution.

## ⚙️ Payload Used
javascript:alert(1)

## 🔎 Analysis
1. User input is stored in the backend  
2. Input is inserted into href attribute  
3. Double quotes are encoded, preventing attribute breaking  
4. Attacker injects javascript: URI scheme  
5. JavaScript executes when the link is clicked  

## 🚀 Steps to Reproduce
1. Navigate to the input/comment section  
2. Enter the following payload:  
   javascript:alert(1)  
3. Submit the input  
4. View the rendered link  
5. Click the link  
6. Observe JavaScript execution  

## ✅ Result
JavaScript alert is triggered when the link is clicked, confirming stored XSS.

## 🧠 Key Learning
Even when quotes are encoded, XSS is possible by injecting malicious URL schemes like javascript: into attributes such as href.

## 🛡️ Prevention
- Validate and restrict allowed URL schemes (http, https only)  
- Encode output properly for attribute context  
- Sanitize stored input  
- Implement Content Security Policy (CSP)  

---

## 📸 Screenshots

<img width="1340" height="689" alt="LAB8_1" src="https://github.com/user-attachments/assets/91ee9905-fd6c-4eac-88e1-adecee93c093" />
<br><br>

**Figure 1: Injecting payload into input field**

<br><br>


<img width="1354" height="633" alt="LAB8_2" src="https://github.com/user-attachments/assets/2d29a6ef-c217-4046-8376-27fcd4a35d11" />
<br><br>

**Figure 2: JavaScript execution after clicking link (Lab Solved)**
