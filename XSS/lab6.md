# 🔐 Lab 6: DOM XSS in jQuery Selector sink Using a hashchange Event

## 🧩 Objective
To exploit a vulnerability where user input from the URL hash is processed by a jQuery selector and executed.

## 🔍 Vulnerability
The application reads input from locations.hash and uses it directly in a Jquery selctor sanitization, allowing execution of arbitrary javascript.

## ⚙️ Payload Used
iframe src="https://url onload = "this.src+='<img src=0 onerror=print()>'"></iframe

## 🔎 Analysis
1. The application linstens for hashchange events
2. It reads input from location.hash
3. The value is passed into a jQuery selector
4. malicious HTML executes javascript

## 🚀 Steps to Reproduce
1. Navigate to the vulnerable page
2. Do DOM manipulation in console check weather jQueRY Accepting hashchange events
3. Then add payload, Then  click on Deliver exploit to victim
4. Observe javascript execution

## ✅ Result
JavaScript alert is triggered, confirming DOM based XSS via jQuery selector.

## 🧠 Key Learning
Using untrusted input inside jQuery slectors can lead to DOM XSS. especially when processing location.hash.

## 🛡️ Prevention
- Avoid using user input in jQuery selectors  
- Sanitize and validate input before DOM usage  
- Use safe DOM APIs  
- Implement Content Security Policy (CSP)  

---

## 📸 Screenshots

<img width="1363" height="672" alt="LAB6_2" src="https://github.com/user-attachments/assets/6cf73849-66b4-4093-b080-e46d27b76cc1" />
<br><br>

**Figure 1: Manipulating DOM by writing text on the main page**

<br><br>

<img width="1365" height="683" alt="LAB6_3" src="https://github.com/user-attachments/assets/0d5a694b-e733-4dec-9229-56aa8569de6d" />
<img width="1364" height="665" alt="LAB6_4" src="https://github.com/user-attachments/assets/0bb76a40-8f02-43bb-baa2-26bee9f5f814" />

<br><br>

**Figure 2: Alter box pop up by console code**

<br><br>

<img width="1342" height="655" alt="LAB6_6" src="https://github.com/user-attachments/assets/3c053010-61fe-4c34-a383-493ca7433274" />
<br><br>

**Figure 3: Injecting payload in the Exploit server**
<br><br>

<img width="1357" height="666" alt="LAB6_5" src="https://github.com/user-attachments/assets/24f602cb-75ac-4d15-92ce-47012facd84a" />
<br><br>

**Figure 4: Print out page after click on view exploit**
<br><br>

<img width="1354" height="674" alt="LAB6_7" src="https://github.com/user-attachments/assets/ba66cb75-ed7d-4bd9-86f8-d9331a7312ef" />
<br><br>

**Figure 5: Successful JavaScript execution via injected iframe (Lab Solved)**
