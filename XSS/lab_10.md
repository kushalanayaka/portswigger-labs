# 🔐 Lab 10: DOM XSS in document.write Sink Using location.search Inside a Select Element.

## 🧩 Objective
To exploit a DOM-based XSS vulnerability where user input is written into a `<select>` element using `document.write`.

## 🔍 Vulnerability
The application uses `document.write` to insert user input from `location.search` into a `<select>` element without sanitization, allowing HTML injection and JavaScript execution.

## ⚙️ Payload Used
/select><img src="0" onerror=alert()">


## 🔎 Analysis
1. User input is read from location.search  
2. Input is written into the page using document.write  
3. Injection occurs inside a `<select>` element  
4. The attacker closes the `<select>` tag  
5. A `<script>` tag is injected  
6. The browser executes the JavaScript  

## 🚀 Steps to Reproduce
1. Navigate to the vulnerable page  
2. Modify the URL parameter:  
   ?productId=/select><img src="0" onerror=alert()">
3. Press Enter  
4. Observe JavaScript execution  

## ✅ Result
A JavaScript alert is triggered, confirming DOM-based XSS.

## 🧠 Key Learning
When user input is placed inside structured HTML elements like `<select>`, attackers can break out of the context and inject executable code.

## 🛡️ Prevention
- Avoid using document.write with untrusted input  
- Properly sanitize and encode input  
- Use safe DOM methods like textContent  
- Implement Content Security Policy (CSP)  

---

## 📸 Screenshots

<img width="1351" height="691" alt="LAB10_1" src="https://github.com/user-attachments/assets/5655c920-1b4f-4c60-b3e4-a77b97f8aff4" />

**Figure 1: Injecting payload into URL parameter**

<br>

<img width="1350" height="681" alt="LAB10_2" src="https://github.com/user-attachments/assets/8520b134-dd76-4eef-b52a-30885d881d87" />

**Figure 2:JavaScript execution after closing select tag (Lab Solved)**

