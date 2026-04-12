# 🔐 Lab 17: Reflected XSS in Canonical Link Tag

## 🧩 Objective
To exploit a vulnerability where user input is injected into href attribute of cononical link tag.

## 🔍 Vulnerability
The application reflects user input inside the href attribute of a `<link rel=canonical">` tag without proper
sanitaization. allowing attribute injection and javascript execution.

## ⚙️ Payload Used
`'accesskey='x' onclick='alert(1)'`

## 🔎 Context
- **Source:** User input (URL parameter)  
- **Sink:** `<link>` tag attribute (href)  
- **Type:** Reflected XSS (attribute context)  

## 🔎 Analysis
1. User input is placed inside the href attribute  
2. Angle brackets are not needed since we are already inside a tag  
3. Attacker breaks out of attribute using `"`  
4. Injects an event handler (`onclick`)  
5. JavaScript executes when the element loads  

## 💡 Payload Explanation
- `'` → closes the existing attribute value  
- `accesskey='x'` → assings a keyboard shortcut to the element
- `onclick='alert(1)'` → executes JavaScript execution  when triggered.

## 👉 How it works:
- The payload breaks out of the href attribute  
- Adds a new attribute `<link>` tag  
- When the browser processes the element, the event triggers  
- JavaScript executes  

## 👉 Why this payload works:
- The application does not escape quotes properly  
- Attribute injection is possible  
- even non-interactive elements can be exploited using accesskey.

## 🚀 Steps to Reproduce
1. Navigate to the vulnerable page  
2. Modify the URL parameter:  
   `?'accesskey='x' onclick='aert(1)'`
3. Press Enter  
4. Observe JavaScript execution  

## ✅ Result
JavaScript alert is triggered, confirming XSS via canonical link tag injection.

## 🧠 Key Learning
Even non-interactive elements like `<link>` tags can be exploited if attribute injection is possible.

## 🛡️ Prevention
- Properly escape attribute values  
- Use context-aware output encoding  
- Avoid directly embedding user input into HTML attributes  
- Implement Content Security Policy (CSP)  

---

## 📸 Screenshots
<img width="1346" height="684" alt="LAB17_1" src="https://github.com/user-attachments/assets/30c4a5ae-235c-424b-803a-c1b4d1c2d3fe" />

**Figure 1: Injecting payload into URL parameter and JavaScript execution via accesskey with onclick event (Lab Solved)**

