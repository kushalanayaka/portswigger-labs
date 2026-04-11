# 🔐 Lab 13: Stored DOM XSS

## 🧩 Objective
To exploit a vulnerability where user input is stored on the server and later processed by client-side javascript, leading to executio.

## 🔍 Vulnerability
The application stores user input in server side and later processed it using client side javascript without proper sanitization, allowing execution of the arbitrary javascript.

## ⚙️ Payload Used
`<h1><img src="0" onerror='alert(1)'>Do Comment</h1>`

## 🔎 Context
- **Source:** Stored input (e.g., comment field)  
- **Sink:** DOM manipulation (innerHTML / document.write)  
- **Type:** Stored DOM XSS  

## 🔎 Analysis
1. User input is submitted and stored in the application.
2. The stored input is later loaded in the page.
3. Client side Javascript process the stored data.
4. Input is inserted into the DOM without sanitaization.
5. Browser interprets HTML and executes Javascripts

## 💡 Payload Explanation
- `<img src=x>` → invalid image triggers error  
- `onerror` → executes when image fails to load  
- `alert(1)` → JavaScript execution  

👉 Why this payload:
- Works reliably in DOM-based contexts  
- Does not depend on `<script>` execution  
- Bypasses many basic filters  

## 🚀 Steps to Reproduce
1. Navigate to the comment or input section  
2. Enter the following payload:  
  `<img src=x onerror=alert(1)>`
3. Submit the input  
4. Reload or revisit the page  
5. Observe JavaScript execution  

## ✅ Result
JavaScript alert is triggered when the stored content is rendered, confirming stored DOM XSS.

## 🧠 Key Learning
Stored DOM XSS occurs when user input is saved and later processed insecurely by client-side JavaScript, leading to execution without direct server reflection.

## 🛡️ Prevention
- Sanitize input before storing  
- Avoid unsafe DOM APIs like innerHTML  
- Use safe methods like textContent  
- Implement Content Security Policy (CSP)  

---

## 📸 Screenshots

<img width="1262" height="599" alt="LAB13_1" src="https://github.com/user-attachments/assets/3310fa8a-ab0d-414d-ac59-c44c03c1b59f" />

**Figure 1: Injecting payload into input field**

<br>

<img width="1358" height="668" alt="LAB13_2" src="https://github.com/user-attachments/assets/60131674-e5a1-44eb-af6f-fc9602292b0b" />

**Figure 2: Alert popup after invalid image trigger**

<br>

<img width="1361" height="642" alt="LAB13_3" src="https://github.com/user-attachments/assets/2e6c4b5f-0a90-4426-b1b8-1f1306bda25f" />

**Figure 3: JavaScript execution when page loads (Lab Solved)**
