# 🔐 Lab 1: Reflected XSS into HTML Context (No Encoding)

## 🧩 Objective
To exploit a reflected cross site scripting(XSS) vulnerability where user input is directly embedded into the html response without any encoding.

## 🔍 Vulnerability
The application reflects user input in the HTML response without proper sanitization or encoding, allowing execution od arbitrary javascript.

## ⚙️ Payload Used
<script>alert(1)</script>

## 🔎 Analysis
1. User input is reflected directly into the html page
2. No output encoding is applied
3. Browser interprets input as executable javascripts
4. Scrips executes in victims's browser

## 🚀 Steps to Reproduce
1. Navigate to the search functionality of the application  
2. Enter the following payload in the search box:  
   <script>alert(1)</script>  
3. Submit the request  
4. Observe JavaScript execution in the browser  

## ✅ Result
JavaScript alert box is triggered, confirming successful XSS execution.

## 🧠 Key Learning
Reflected XSS occurs when user input is immediately returned in the response without proper encoding, allowing execution of malicious scripts.

## 🛡️ Prevention
- Encode output based on context (HTML encoding)  
- Validate and sanitize user input  
- Use Content Security Policy (CSP)  
- Avoid directly embedding user input into HTML  

---

## 📸 Screenshots

<img width="1322" height="405" alt="LAB1_3" src="https://github.com/user-attachments/assets/11bd3dde-9c0c-43f5-ac3e-e661e85d50bb" />
<br><br>

**Figure 1: Inputting XSS payload in search field**

<br><br>

<img width="1341" height="654" alt="LAB1_2" src="https://github.com/user-attachments/assets/e28d080b-8df0-4e67-9327-26ba1db76213" />
<br><br>

**Figure 2: Alert box Popup in the page**

<br><br>

<img width="1342" height="691" alt="LAB1_4" src="https://github.com/user-attachments/assets/1415d629-aaa4-4927-a021-63209f54e1e3" />
<br><br>

**Figure 3: JavaScript alert executed in browser (Lab Solved)**
