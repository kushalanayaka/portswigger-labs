# 🔐 Lab 12: Reflected DOM XSS

## 🧩 Objective
To exploit a vulnerability where uer input is processed by client-side Javascript and executed in the browser.

## 🔍 Vulnerability
The application reads user input from the URL and process it using client-side Javascript without proper sanitization, allowing execution of the arbitrary Javascript.

## ⚙️ Payload Used
`\"-alert()}//`

## 🔎 Context
- **Source:** location.search  
- **Sink:** DOM manipulation (e.g., innerHTML / document.write)  
- **Type:** DOM-based Reflected XSS  

## 🔎 Analysis
1. User input is taken from the URL  
2. JavaScript processes the input in the browser  
3. Input is inserted into the DOM without sanitization  
4. HTML is interpreted by the browser  
5. Event handler executes JavaScript  

## 💡 Payload Explanation
- `\"` → escape the qoute(keep string valid initially)
- `-` → breaks into Js expression  
- `alert(1)` → executes JS
- `}` -> closes a block(if one exists in original code)
- `//` -> comments out rest

👉 Why this payload:
- `<script>` may be blocked or not executed  
- Event handlers are more reliable in DOM XSS  

## 🚀 Steps to Reproduce
1. Navigate to the vulnerable page  
2. Modify the URL parameter:  
   `lashuk\"-alert()}//`  
3. Press Enter  
4. Observe JavaScript execution  

## ✅ Result
JavaScript alert is triggered, confirming reflected DOM XSS.

## 🧠 Key Learning
DOM XSS occurs entirely in the browser, and reflected input can still lead to execution if client-side scripts handle it insecurely.

## 🛡️ Prevention
- Avoid inserting untrusted input into the DOM  
- Use safe APIs like textContent instead of innerHTML  
- Sanitize input before DOM usage  
- Implement Content Security Policy (CSP)  

---

## 📸 Screenshots

<img width="1360" height="699" alt="LAB12_1" src="https://github.com/user-attachments/assets/799e53f2-87cd-45ae-9d4e-cd6b8cf35180" />

**Figure 1: Injecting payload into URL parameter in BUrp Suite**

<br>

<img width="1345" height="673" alt="LAB12_2" src="https://github.com/user-attachments/assets/b0720725-3ab1-4f64-b851-9deef9fb7ef8" />

**Figure 2: JavaScript execution via alert event (Lab Solved)**
