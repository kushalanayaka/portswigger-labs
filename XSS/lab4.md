# 🔐 Lab 4: DOM XSS in innerHTML Sink Using source location.search

## 🧩 Objective
Tp exploit the vulnearbility using innerHTML without encoding.

## 🔍 Vulnerability
The application reads user input from location.search and inserts it into the DOM using innerHTML, allowing execution of arbitrary HTML and JavaScript.

## ⚙️ Payload Used
img src=x onerror=alert(1)

## 🔎 Analysis
1. The application reads input from location.search  
2. The value is inserted into the DOM using innerHTML  
3. innerHTML parses input as HTML  
4. Malicious HTML with event handlers executes JavaScript  
5. Script runs in the browser  

## 🚀 Steps to Reproduce
1. Navigate to the vulnerable page  
2. Modify the URL parameter:  
   ?search=<img src=x onerror=alert(1)
3. Press Enter  
4. Observe JavaScript execution  

## ✅ Result
JavaScript alert is triggered, confirming DOM-based XSS via innerHTML.

## 🧠 Key Learning
innerHTML is dangerous when used with untrusted input, as it parses and executes HTML including JavaScript event handlers.

## 🛡️ Prevention
- Avoid using innerHTML with user input  
- Use textContent or innerText instead  
- Sanitize input before inserting into DOM  
- Use Content Security Policy (CSP)  

---

## 📸 Screenshots

<img width="1350" height="658" alt="LAB4_1" src="https://github.com/user-attachments/assets/9f0dc3a5-aaac-4455-89fc-53a722c3b715" />
<br><br>

**Figure 1: Injecting payload via URL parameter**
<br><br>
<img width="1356" height="677" alt="LAB4_2" src="https://github.com/user-attachments/assets/66815fce-e7e3-4a56-a33d-c09e1f4bb6ad" />
<br><br>

**Figure 2: Alter box and JavaScript execution via onerror event (Lab Solved)**
