# 🔐 Lab 18: SQL Injection with Filter Bypass via XML Encoding

## 🧩 Objective
To exploit SQL Injection with Filter Bypass via XML Encoding

## 🔍 Vulnerability
The application processes user input via XML and fails to properly sanitize encoded characters, allowing SQL Injection through XML-encoded payloads.

## ⚙️ Payload Used
1 UNION SELECT username || ':' || password FROM users

## 🔎 Analysis
1. The application blocks standard SQL Injection characters  
2. XML encoding is used to bypass filters  
3. Encoded characters are decoded by the XML parser  
4. The decoded payload is executed in the SQL query  

## 🚀 Steps to Reproduce
1. Intercept the request using Burp Suite  
2. Identify XML request body  
3. Modify parameter using encoded payload:
  - 1 UNION SELECT username || ':' || password FROM users  
4. Send the request
5. Use Hackvertor extension
   - If it is not there
     - Go to extension -> search Hackvertor -> install
   - To encode
     - Right click -> encode -> hex-entities
6. Observe successful injection  

## ✅ Result
Successfully bypassed input filters and executed SQL Injection using XML encoding.

## 🧠 Key Learning
Encoding techniques can bypass input validation mechanisms, allowing SQL Injection even when filters are in place.

## 🛡️ Prevention
- Use parameterized queries (prepared statements)  
- Validate and sanitize decoded input  
- Avoid trusting encoded input  
- Implement strict input validation  

---

## 📸 Screenshots

<img width="1355" height="698" alt="LAB18_1" src="https://github.com/user-attachments/assets/60fb0de0-69c7-4c06-b30e-74157aa25bc2" />
<br><br>

**Figure 1: Injecting XML-encoded payload**

<br><br>

<img width="1364" height="696" alt="LAB18_2" src="https://github.com/user-attachments/assets/2b1220d2-dff4-4aad-b7e4-666b12007a76" />
<br><br>

**Figure 2: Payload decoded and executed username and password by backend**

<br><br>

<img width="1348" height="628" alt="LAB18_3" src="https://github.com/user-attachments/assets/f2bac4ac-9aa9-477a-b0cb-ce24baafd107" />
<br><br>

**Figure 3: Successful SQL Injection via XML encoding (Lab Solved)**
