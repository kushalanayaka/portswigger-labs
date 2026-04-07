# 🔐 Lab 9: Reflected XSS into a JavaScript String with Angle Brackets HTML-Encoded

## 🧩 Objective
To exploit a reflected XSS vulnerability where user input is embeddedinisde a javascript string with abgle brackets encoded.

## 🔍 Vulnerability
The application reflects user input inside a JavaScript string without proper escaping, allowing attackers to break out of the string and execute arbitrary JavaScript.

## ⚙️ Payload Used
'+ alert() +'

## 🔎 Analysis
1. User input is inserted inside a javascript sting
2. Angle brackets are encoded, preventing HTML injection
3. JavaScript string context is not properly escaped
4. Attacker breaks out using '
5. Injects Javascript code
6. USes // to comment out remaining code
   
## 🚀 Steps to Reproduce
1. Navigate to the vulnerable page  
2. Enter the following payload:  
   '+ alert() +' 
3. Submit the input  
4. Observe JavaScript execution  

## ✅ Result
JavaScript alert is triggered, confirming XSS in JavaScript string context.

## 🧠 Key Learning
Even when HTML tags are encoded, XSS is possible by exploiting JavaScript context and breaking out of strings.

## 🛡️ Prevention
- Escape user input for JavaScript context  
- Use JSON encoding or safe APIs  
- Avoid embedding user input directly into scripts  
- Implement Content Security Policy (CSP)  

---

## 📸 Screenshots

<img width="1311" height="597" alt="LAB9_1" src="https://github.com/user-attachments/assets/296afe52-c6ba-4b85-b78c-aa62f2cfc4c1" />
<br><br>

**Figure 1: Injecting payload into input field**


<br><br>

<img width="1343" height="674" alt="LAB9_3" src="https://github.com/user-attachments/assets/2e6cbe9a-9318-46fb-abbe-4739a2d03e86" />
<br><br>

**Figure 2: JavaScript execution after breaking out of string (Lab Solved)**
