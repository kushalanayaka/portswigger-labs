# 🔐 Lab 2: Stored XSS into HTML Context (No Encoding)

## 🧩 Objective
To exploit a stored Cross Site scripting (XSS) vulnerability where user input stored on the server and later rendered in the HTML response without encoding.

## 🔍 Vulnerability
The application stored user input(e.g., comment) and displays it in the the HTML page without proper sanitization or encoding, allowing execution of arbitary javascript.

## ⚙️ Payload Used
<script>alert(1)</script>

## 🔎 Analysis
1. user input is stored in the backed database
2. Input is rendered in HTML without encoding
3. Browser interpets input as javascript
4. Script execute whenever the page is load.
   
## 🚀 Steps to Reproduce
1. Navigate to the comment or input section of the application  
2. Enter the following payload:  
   <script>alert(1)</script>  
3. Submit the input  
4. Reload or revisit the page  
5. Observe JavaScript execution  

## ✅ Result
Javascript alert executes whenever the page is viewed, confirming stored XSS.

## 🧠 Key Learning
Stored XSS is more dangerous than reflected XSS becuase the paload persists and affect all users who view the page.

## 🛡️ Prevention
- Encode output based on context (HTML encoding)  
- Validate and sanitize user input  
- Use Content Security Policy (CSP)  
- Avoid storing unsafe input  

---

## 📸 Screenshots
<img width="1350" height="676" alt="LAB2_1" src="https://github.com/user-attachments/assets/da0c96cc-c7dc-41bf-96c9-d065950369b9" />

<br><br>

**Figure 1: Injecting XSS payload into comment field**

<br><br>


<img width="1348" height="672" alt="LAB2_2" src="https://github.com/user-attachments/assets/3b4f4901-f12f-414d-8be5-702b94aec548" />
<br><br>

**Figure 2: JavaScript executed when page loads (Lab Solved)**
