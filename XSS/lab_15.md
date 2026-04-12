# 🔐 Lab 15: Reflected XSS into HTML Context with All Tags Blocked Except Custom Ones

## 🧩 Objective
To exploit a vulnerability by bypassing stricy fitering that blocks standard HTML tags and allows anly custom tags.

## 🔍 Vulnerability
The application filters out all standard HTML tags but allows custom tags, but it fails to properly sanitize event atrributes, allowing javascript execution.

## ⚙️ Payload Used
`<custom-tag onfocus='alert(document.cookie)' id='x' tabindex='1'>`

## 🔎 Context
- **Source:** User input (search parameter)  
- **Sink:** HTML rendering  
- **Type:** Reflected XSS with strict tag filtering  

## 🔎 Analysis
1. The application blocks common HTML tags  
2. Custom/non-standard tags are still allowed  
3. Event handlers like `onfocus` are not filtered  
4. `tabindex` makes the element focusable  
5. JavaScript executes when the element receives focus  

## 💡 Payload Explanation
- `<custom-tag>` → custom HTML tag allowed by the filter  
- `onfocus` → Its a evenrt handler that triggers when the element gain focus  
- `tabindex=1` → makes the element focusable  
- `alert(document.cookie)` → demonstrates access to sensitive data(cookie) 

## 👉 How it works:
- The custom tag is rendered in the DOM  
- The element becomes focusable using `tabindex`  
- When the user presses TAB or clicks the element, `onfocus` triggers  
- JavaScript executes  

## 👉 Why this payload works:
- Filters block known tags but allow unknown/custom tags  
- Event handlers are not fully restricted  
- Attack leverages browser behavior instead of standard tags  

## 🚀 Steps to Reproduce
1. Navigate to the vulnerable page  
2. Enter the following payload:  
   <xss id=x onfocus=alert(1) tabindex=1>  
3. Submit the input  
4. Press TAB or click the element  
5. Observe JavaScript execution  

## ✅ Result
JavaScript alert is triggered when the element gains focus, confirming successful filter bypass and XSS.

## 🧠 Key Learning
Blocking known HTML tags is not sufficient. Attackers can use custom tags and event handlers to execute JavaScript.

## 🛡️ Prevention
- Use strict allowlist-based HTML sanitization  
- Remove or sanitize event handler attributes  
- Encode output based on context  
- Implement Content Security Policy (CSP)  

---

## 📸 Screenshots

<img width="1353" height="672" alt="LAB15_6" src="https://github.com/user-attachments/assets/cafec157-7561-477e-865d-f305c18e3541" />

**Figure 1: Injecting payload using custom tag**

<br>

<img width="1361" height="683" alt="LAB15_1" src="https://github.com/user-attachments/assets/b4239848-ace8-447f-8c70-3dfb757484a3" />

**Figure 2: Payload rendered in DOM**

<br>

<img width="1362" height="676" alt="LAB15_2" src="https://github.com/user-attachments/assets/d8f2a5b0-a1b5-493d-8db3-a02f43cc3c9c" />

**Figure 3: JavaScript execution via onfocus event (Lab Solved)**
