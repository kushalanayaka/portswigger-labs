# 🔐 Lab 3: DOM XSS in document.write Sink Using source location.search

## 🧩 Objective
To exploit a DOM based Cross Site Scripting(XSS) vulnerability where user input from the URL is written into the page using document.write sanitaization.

## 🔍 Vulnerability
The application uses javascript to read user input from loaction.search and writes it directly into the HTML.write, allowing execution of arbitrary javascript.

## ⚙️ Payload Used
<script>alert(1)</script>

## 🔎 Analysis
1. The application reads input from location.search (URL parameter)  
2. The value is directly passed to document.write  
3. No sanitization or encoding is applied  
4. Browser interprets input as HTML/JavaScript  
5. Script executes in the browser  

## 🚀 Steps to Reproduce
1. Navigate to the vulnerable page  
2. Modify the URL parameter:  
   ?search=<script>alert(1)</script>  
3. Press Enter  
4. Observe JavaScript execution  

## ✅ Result
JavaScript alert is executed, confirming DOM-based XSS.

## 🧠 Key Learning
DOM XSS occurs when client-side JavaScript processes user input and writes it to the page without proper validation or encoding.

## 🛡️ Prevention
- Avoid using document.write with untrusted input  
- Use safe DOM methods (textContent, innerText)  
- Implement proper input sanitization  
- Use Content Security Policy (CSP)  

---

## 📸 Screenshots

<img width="1353" height="637" alt="LAB3_3" src="https://github.com/user-attachments/assets/c4470192-5972-4dc2-8c61-40d612d31faf" />
<br><br>

**Figure 1: Injecting payload via URL parameter**

<br><br>

<img width="1364" height="665" alt="LAB3_4" src="https://github.com/user-attachments/assets/fbec8c2d-2b65-42f7-ab1a-2576b7f1ba2e" />
<br><br>

**Figure 2: Payload processed in document.write popups aler box**

<br><br>

<img width="1363" height="673" alt="LAB3_5" src="https://github.com/user-attachments/assets/992849af-b364-4533-8c78-b43c7051c2ed" />
<br><br>

**Figure 3: JavaScript execution in browser (Lab Solved)**
