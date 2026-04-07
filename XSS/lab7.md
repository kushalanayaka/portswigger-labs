# 🔐 Lab 7: Reflected XSS into Attribute with Angle Brackets HTML-Encoded

## 🧩 Objective
To exploit the reflected XSS vulnerability in an HTML attribute where angle bractes are encoded, but atrribute injection is still possible.

## 🔍 Vulnerability
The application reflects user input inside an HTML attribute. Although angle bractes(<, >) are encoded, the application does not properly sanitize attribute context, allowing injection of event handlers.

## ⚙️ Payload Used
" onmouseover="alert(1)

## 🔎 Analysis
1. User input is placed inside an HTML attribute
2. Angle brackets are encoded, preventing <script> injection
3. Attribute context is not properly sanitized
4. Attacker breaks out of attribute using "
5. Injects event handler (onmouseover)
6. JavaScripts executes on user interaction

## 🚀 Steps to Reproduce
1. Navigate to the vulnerable page  
2. Enter the following payload:  
   " onmouseover="alert(1)  
3. Submit the input  
4. Hover over the affected element  
5. Observe JavaScript execution  

## ✅ Result
JavaScript alerts is triggered when hovering, confirming XSS via atrribute injection.

## 🧠 Key Learning
Even when angle brackets are encoded, XSS is possible by breaking out the atrribute context and injecting event handlers.

## 🛡️ Prevention
- Properly encode output for attribute context
- Escape quotes inside attributes
- use safe tempering frameworks
- Implement Content Security Policy(CSP)  

---

## 📸 Screenshots

<img width="1357" height="684" alt="LAB7_1" src="https://github.com/user-attachments/assets/2f3a6fdc-922e-4a41-94ff-7e42ee14dadb" />
<br><br>

**Figure 1: Injecting payload into input field**


<br><br>

<img width="1360" height="652" alt="LAB7_2" src="https://github.com/user-attachments/assets/b568e21e-ff7e-482a-860d-2af2034969b2" />
<br><br>

**Figure 2: JavaScript execution via onmouseover event (Lab Solved)**
