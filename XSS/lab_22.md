# 🔐 Lab 22: Reflected XSS with Event Handlers and href Attributes Blocked

## 🧩 Objective
To exploit a reflected XSS vulnerability where event handlers and href attributes are blocked, requring alternative execution techniques.

## 🔍 Vulnerability
The application filters out:
- Event handler attributes (e.g., onload, onclick)  
- JavaScript URLs in href attributes
- However, it fails to properly sanitize SVG content, allowing execution of Javascript via embedded script tag.

## ⚙️ Payload Used

`(https://YOUR-LAB-ID.web-security-academy.net/?search=%3Csvg%3E%3Ca%3E%3Canimate+attributeName%3Dhref+values%3Djavascript%3Aalert(1)+%2F%3E%3Ctext+x%3D20+y%3D20%3EClick%20me%3C%2Ftext%3E%3C%2Fa%3E)`
## 🔎 Context
- **Source:** User input (search parameter)  
- **Sink:** HTML/SVG rendering  
- **Type:** Reflected XSS (filter bypass)  

## 🔎 Analysis
1. Common XSS vectors (event handlers, href) are blocked  
2. SVG tags are still allowed  
3. `<script>` inside SVG is not filtered  
4. Browser executes JavaScript inside SVG  
5. XSS is successfully triggered  

## 💡 Payload Explanation
- `<svg>` → container for SVG content 
- `<a>` → anchor element that can hold a link
- `<animate>` → dynamically modifies attributes
- `attributeName="href"`  → target the href attribute
- `values="javascript:alert(1)"` → injects JavaScript URI
- `<text>` → creates visible clickable content

## 👉 How it works:
-  The application blocks direct use of `href` and event handlers
-  The payload uses SVG animation to dynamically assign a malicious `href`
-  This bypasses filtering becuase the attribute is not directly present in the HTML
-  When the user click the text, the javascript executes 

## 👉 Why this payload works:
- Filters do not accounts for dynamic attribute changes 
- SVG animation allows runtime modification of attributes
- The browser executes javascript from the injected href

## 🚀 Steps to Reproduce
1. Navigate to the vulnerable page  
2. Enter the following payload:  
   <svg><script>alert(1)</script></svg>  
3. Submit the input  
4. Observe JavaScript execution  

## ✅ Result
JavaScript alert is triggered, confirming XSS via SVG script injection.

## 🧠 Key Learning
Blocking event handlers and href attributes is not enough. Attackers can exploit alternative execution contexts like SVG.

## 🛡️ Prevention
- Sanitize all HTML and SVG content  
- Remove or block `<script>` tags entirely  
- Use strict allowlist-based filtering  
- Implement Content Security Policy (CSP)  

---

## 📸 Screenshots

<img width="1361" height="679" alt="LAB27" src="https://github.com/user-attachments/assets/32cdffa0-8b6a-4079-a3d7-aa38f2b8ced3" />

**Figure 1: Injecting SVG payload,JavaScript execution (Lab Solved)**
