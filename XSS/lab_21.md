# 🔐 Lab 21: Reflected XSS into a Template Literal with Angle Brackets, Single, Double Quotes, Backslash and Backticks Unicode-Escaped

## 🧩 Objective
To exploit a reflected XSS vulnerability inside a JavaScript template literal despite extensive encoding protections.

## 🔍 Vulnerability
The application embeds user input inside a JavaScript template literal and applies Unicode escaping to:
- Angle brackets (`< >`)  
- Single and double quotes (`' "`)  
- Backslashes (`\`)  
- Backticks (`` ` ``)
- However, it fails to sanitize template literal expressions, allowing execution of JavaScript.

## ⚙️ Payload Used
`${alert(1)}`

## 🔎 Context
- **Source:** User input (URL parameter)  
- **Sink:** JavaScript template literal  
- **Type:** Reflected XSS (template literal injection)  

## 🔎 Analysis
1. User input is inserted inside a template literal  
2. Special characters are escaped  
3. Template literal expressions (`${}`) are still evaluated  
4. Attacker injects JavaScript expression  
5. Code executes immediately  

## 💡 Payload Explanation
- `${}` → template literal expression syntax  
- `alert(1)` → JavaScript execution  

👉 How it works:
- Template literals evaluate expressions inside `${}`  
- The injected expression runs even if characters are escaped  
- No need to break out of the string  

👉 Why this payload works:
- The application protects characters but not logic  
- Template literal evaluation is not restricted  
- JavaScript expressions execute automatically  

## 🚀 Steps to Reproduce
1. Navigate to the vulnerable page  
2. Modify the URL parameter:  
   `?search=${alert(1)}`
3. Press Enter  
4. Observe JavaScript execution  

## ✅ Result
JavaScript alert is triggered, confirming XSS via template literal injection.

## 🧠 Key Learning
Escaping characters is not sufficient in template literals. Expression injection using `${}` can still lead to execution.

## 🛡️ Prevention
- Avoid embedding user input in template literals  
- Escape or sanitize `${}` patterns  
- Use safe templating or encoding methods  
- Implement Content Security Policy (CSP)  

---

## 📸 Screenshots

<img width="1356" height="675" alt="LAB21_1" src="https://github.com/user-attachments/assets/4e1ae06a-0103-4f86-b254-63228ae75b3f" />

**Figure 1: Injecting template literal payload and JavaScript execution via ${} expression (Lab Solved)**

