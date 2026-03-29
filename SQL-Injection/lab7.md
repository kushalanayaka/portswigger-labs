# 🔐 Lab 7: Determing the number of columns using UNION attack.

## 🧩 Objective
To determine the number of columns returned by the SQL query using UNION based SQL injection attack.

## 🔍 Vulnerability
The application is vulnerable to SQL Injection in the product category parameter, allowing manipulation of the SQL query.

## ⚙️ Payload Used
### Way 1
- ' ORDER BY 1-- => 200 OK
- ' ORDER BY 2-- => 200 OK
- ' ORDER BY 3-- => 200 OK
- ' ORDER BY 4-- => 500 SERVER ERROR (means only 3 columns)

 ### Way 2
 - ' UNION SELECT NULL-- => 500 SERVER ERROR
 - ' UNION SELECT NULL, NULL-- => 500 SERVER ERROR
 - ' UNION SELECT NULL,NULL,NULL-- => 200 OK

## 🔎 Analysis
1. Inject ORDER BY cluase incrementally
2. Increase cloumns number until an error occurs
3. The last successful number indicates total columns
   
## 🚀 Steps to Reproduce
1. Navigate to the product category page  
2. Intercept the request using Burp Suite  
3. Send the request to Repeater and modify the parameter using commands.  
4. Send the request and analyze the response
5. Identify the number of columns based on the last successful query

## ✅ Result
The number of columns in the query is successfully determined.

## 🧠 Key Learning
Detemining the correct number of cloumns is essentail fro performing UNION based SQL injection attacks

## 🛡️ Prevention
- Use parameterized queries (prepared statements)  
- Implement proper input validation
- Avoid exposing database errors and sensitive data  

---

## 📸 Screenshots
<img width="1355" height="649" alt="LAB7_1" src="https://github.com/user-attachments/assets/1d797390-67f2-4897-b91d-c612f306a402" />

**Figure 1:Determining number of columns using ORDER BY payload WAY 1**

<br><br>
<img width="1352" height="669" alt="LAB7_2" src="https://github.com/user-attachments/assets/59151f22-7e26-422f-b8aa-ed92461e7a49" />

**Figure 2:Determining number of columns using UNION payload WAY 2**

<br><br>
<img width="1359" height="680" alt="LAB7_3" src="https://github.com/user-attachments/assets/7f959dd4-2ce7-42ba-aade-f6b017dd8085" />

**Figure 6: Successful Lab Solved**
