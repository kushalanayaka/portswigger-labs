# 🔐 Lab 16: Reflected XSS with Some SVG Markup Allowed

## 🧩 Objective
To exploit a vulnerability by leveraging allowed SVG markup to execute JavaScript.

## 🔍 Vulnerability
The application filters most HTML tags but allows certain SVG elements. It fails to properly sanitize SVG-specific event attributes, enabling JavaScript execution.

## ⚙️ Payload Used
`<svg><animatetransform onbegin=alert(1)></animatetransform></svg>`

## 🔎 Context
- **Source:** User input (search parameter)  
- **Sink:** HTML/SVG rendering  
- **Type:** Reflected XSS with SVG filter bypass  

## 🔎 Analysis
1. The application blocks standard HTML tags  
2. Use Intruder to find some like SVG tags and are still allowed  
3. SVG supports animation and event attributes  
4. The `onbegin` event is not filtered  used intruder for this.
5. JavaScript executes automatically when the animation starts  

## 💡 Payload Explanation
- `<svg>` → allowed container for SVG content  
- `<animatetransform>` → SVG animation element  
- `onbegin` → event triggered when animation starts  
- `alert(1)` → JavaScript execution  

👉 How it works:
- The SVG element is rendered by the browser  
- The animation element initializes  
- The `onbegin` event is triggered automatically  
- JavaScript executes without user interaction  

👉 Why this payload works:
- Filters often overlook SVG-specific elements  
- Event handlers in SVG are less commonly blocked  
- Executes automatically without user interaction  

## 🚀 Steps to Reproduce
1. Navigate to the vulnerable page
2. Use Burp Suite to find the non filter tag and event.
3. Enter the following payload:  
   `<svg><animatetransform onbegin=alert(1)></animatetransform></svg> `
4. Submit the input  
5. Observe JavaScript execution  

## ✅ Result
JavaScript alert is triggered, confirming successful XSS via SVG bypass.

## 🧠 Key Learning
Even when HTML is restricted, SVG can provide alternative attack vectors due to its support for scripting and events.

## 🛡️ Prevention
- Sanitize SVG content properly  
- Remove or restrict event attributes  
- Use strict allowlist-based filtering  
- Implement Content Security Policy (CSP)  

---

## 📸 Screenshots

<img width="1345" height="661" alt="LAB16_1" src="https://github.com/user-attachments/assets/0bda29a8-e788-4f85-9cf5-573fd88a4370" />

**Figure 1: Finding non filter HTML tags using Burp suite Intruder**

<br>

<img width="1309" height="669" alt="LAB16_2" src="https://github.com/user-attachments/assets/3c229877-8822-455c-b39e-c8ce8c2c5916" />

**Figure 2: Finding non filter HTML event  using Burp suite Intruder**

<br>

<img width="1349" height="670" alt="LAB16_3" src="https://github.com/user-attachments/assets/b13c81bc-beaf-442b-9b35-e0cf61c64038" />

**Figure 3: JavaScript execution via SVG animation event (Lab Solved)**
