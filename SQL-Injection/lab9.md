# 🔐 Lab 9: Retrieving Data from the Table using UNION attack.

## 🧩 Objective
To retrieve username and password from another table using a UNION based SQL injection attack.

## 🔍 Vulnerability
The application is vulnerable to SQL Injection in the product category parameter, allowing attackers to manipulate queries and extract data from the database.

## ⚙️ Payload Used
- 'ORDER BY 3--
- ' UNION SELECT 'a', 'a'--
' UNION SELECT username, password FROM users--

## 🔎 Analysis
1. Determine the number of columns in the query  
2. Identify which columns accept text data  
3. Use UNION SELECT to query the users table  
4. Extract username and password columns  

## 🚀 Steps to Reproduce
1. Navigate to the product category page  
2. Intercept the request using Burp Suite  
3. Send the request to Repeater  
4. Modify the parameter with:
   ' UNION SELECT username, password FROM users--  
5. Send the request  
6. Observe the response displaying usernames and passwords  

## ✅ Result
Successfully retrieved usernames and passwords from the users table.

## 🧠 Key Learning
SQL Injection can be used to extract sensitive data from other database tables, leading to full compromise of user accounts.

## 🛡️ Prevention
- Use parameterized queries (prepared statements)  
- Implement strict input validation  
- Apply least privilege to database accounts  
- Avoid exposing sensitive data in responses  

---

## 📸 Screenshots
<img width="1357" height="667" alt="LAB9_1" src="https://github.com/user-attachments/assets/a6f9876c-c298-4d5f-8f07-aa5e1a586501" />
<br><br>

**Figure 1: Preparing ORDER BY SQL Injection payload(server error after order by 3 value means 2 cloumns)**

<br><br>

<img width="1365" height="669" alt="LAB9_2" src="https://github.com/user-attachments/assets/2febbc9c-ec7c-4ae7-8fe2-d591aba7ab8f" />
<br><br>

**Figure 2: Identify which columns accept text data using UNION  attack**

<br><br>
<img width="1338" height="645" alt="LAB9_3" src="https://github.com/user-attachments/assets/115a3be6-25e8-4122-b70a-38edff536716" />
<br><br>

**Figure 3: Displaying usernames and passwords in response**

<br><br>
<img width="1337" height="656" alt="LAB9_4" src="https://github.com/user-attachments/assets/5731bb56-418a-4ed6-9bed-ead468977bb6" />
<br><br>

**Figure 4: Using usernames and passwords to login as a administrator**
<br><br>

<img width="1342" height="659" alt="LAB9_6" src="https://github.com/user-attachments/assets/cccb072f-22db-4a5e-a83e-f5d3c2f499c5" />
<br><br>

**Figure 4: Using Burp suite to intercept the reuest and extract the sensitive data**
<br><br>

<img width="1329" height="667" alt="LAB9_5" src="https://github.com/user-attachments/assets/d82ed99c-9fa4-40dd-ab64-9c972d10e931" />
<br><br>
**Figure 5: Successful logged in as a administrator**
