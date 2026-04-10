# 🔐 Lab 11: DOM XSS in AngularJS Expression with Angle Brackets and Double Quotes HTML-Encoded

## 🧩 Objective
To exploit a DOM-based XSS vulnerability using AngularJS expression injection where angle brackets and double quotes are HTML-encoded.

## 🔍 Vulnerability
The application uses AngularJS to render user input. Although angle brackets and double quotes are encoded, AngularJS expressions are still evaluated, allowing execution of arbitrary JavaScript.

## ⚙️ Payload Used
{{$on.constructor('alert(1)')()}}

## 🔎 Context
- **Source:** location.search  
- **Sink:** AngularJS expression evaluation  
- **Framework:** AngularJS  

## 🔎 Analysis
1. User input is processed by AngularJS  
2. HTML tags are encoded, preventing traditional XSS  
3. AngularJS expressions (`{{ }}`) are still evaluated  
4. Attacker injects malicious AngularJS expression  
5. JavaScript is executed via constructor  

## 💡 Payload Explanation
- `{{ ... }}` → AngularJS expression syntax  
- `$on` → refers to the object constructor  
- `.constructor` → accesses the Function constructor  
- `'alert(1)'` → JavaScript code as string  
- `()` → executes the function  

👉 Full flow:
- Access Function constructor  
- Create new function with `alert(1)`  
- Execute it  

## 🚀 Steps to Reproduce
1. Navigate to the vulnerable page  
2. Modify the URL parameter:  
   ?search={{$on.constructor('alert(1)')()}}  
3. Press Enter  
4. Observe JavaScript execution  

## ✅ Result
JavaScript alert is triggered, confirming DOM-based XSS via AngularJS expression injection.

## 🧠 Key Learning
Even when HTML characters are encoded, frameworks like AngularJS can introduce new attack surfaces through expression evaluation.

## 🛡️ Prevention
- Disable AngularJS expression evaluation for user input  
- Use strict contextual escaping  
- Upgrade frameworks and avoid legacy AngularJS  
- Implement Content Security Policy (CSP)  

---

## 📸 Screenshots

<img width="1362" height="681" alt="LAB11_1" src="https://github.com/user-attachments/assets/3bad44a9-b430-4046-8892-a13beee8c9df" />
<br>

**Figure 1: Payload processed by AngularJS expression and JavaScript execution via AngularJS (Lab Solved)**
