# 🔐 Lab 20: Stored XSS into onclick Event with Angle Brackets and Double Quotes HTML-Encoded and Single Quotes and Backslash Escaped

## 🧩 Objective
To exploit a vulnerability within a JavaScript context inside an `onclick` event handler despite multiple encoding protections.

## 🔍 Vulnerability
The application stores user input and embeds it inside a JavaScript string within an `onclick` attribute. It attempts to prevent XSS by:
- Encoding angle brackets (`< >`) and double quotes (`"`)
- Escaping single quotes (`'`) and backslashes (`\`)
- However, improper handling of escape sequences allows breaking out of the JavaScript string and executing arbitrary code.

## ⚙️ Payload Used
`http://foo?&apos;-alert()-&apos;`

## 🔎 Context
- **Source:** Stored input (e.g., comment field)  
- **Sink:** JavaScript inside `onclick` attribute  
- **Type:** Stored XSS (JavaScript escape bypass)  

## 🔎 Analysis
1. User input is stored in the application  
2. The stored input is inserted into a JavaScript string inside `onclick`  
3. Single quotes are escaped (e.g., `\'`)  
4. Attacker injects a backslash to neutralize escaping  
5. The string is terminated  
6. JavaScript executes when the element is clicked  

## 💡 Payload Explanation
- `&apos;` → HTML entity for single quote(`'`)
- `http://foo?` → Valid string to maintain syntax
- `-alert(1)` → executes JavaScript  
- `-` → used to chain expressions without breaking syntax  

👉 How it works:
- The application encodes single qoutes, but they are decoded by the browser
- The payload injects a valid javascript expression inside the string
- Instead of breaking the string, it leverages javascript arithmetic evaluation
- The `alert()` function executes as part of the expression

👉 Why this payload works:
- It does not rely on breaking out of the string
- It used Javascript evaluation logic instead
- It bypasses escaping mechanisms applied to quotes and backslashes

## 🚀 Steps to Reproduce
1. Navigate to the input/comment section  
2. Enter the following payload: `http://foo?&apos;-alert()-&apos;`
3. Submit the input  
4. Click the affected element  
5. Observe JavaScript execution  

## ✅ Result
A JavaScript alert is triggered on click, confirming stored XSS via escape bypass.

## 🧠 Key Learning
Even when multiple encoding techniques are applied, improper handling of escape sequences in JavaScript contexts can still lead to XSS.

## 🛡️ Prevention
- Use strict JavaScript encoding (e.g., JSON encoding)  
- Avoid embedding user input directly into event handlers  
- Use secure templating frameworks  
- Implement Content Security Policy (CSP)  

---

## 📸 Screenshots

<img width="1365" height="676" alt="LAB20_1" src="https://github.com/user-attachments/assets/46a314da-2773-49d4-8e82-43cdc6ce7c1f" />

**Figure 1: Injecting payload into input field**

<br>

<img width="1344" height="679" alt="LAB20_2" src="https://github.com/user-attachments/assets/206ea1c0-83c2-44d7-95ee-ca751f1c4404" />

**Figure 2: JavaScript execution after clicking element (Lab Solved)**

