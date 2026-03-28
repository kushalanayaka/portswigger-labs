# 🔐 Lab 4: MySQL and Microsoft DB Version Enumeration

## 🧩 Objective
To display the database type and version string.

## 🔍 Vulnerability
The application is vulnerable to SQL Injection in the product category parameter, allowing attackers to execute arbitrary SQL queries.

## ⚙️ Payload Used
' ORDER BY 3--  
' UNION SELECT 'a', 'a'--  
' UNION SELECT @@vesion, NULL--

## 🔎 Analysis
1. Determine the number of columns using first payload. 3 - 1 = 2  
2. Determine the data types of the columns using second payload  
3. Both MySQL and Microsoft have same SELECT @@version command  
4. Output the version of the database  

## 🚀 Steps to Reproduce
1. Navigate to the product category page  
2. Intercept the request using Burp Suite  
3. Send the request to Repeater and modify the parameter:  
   ' UNION SELECT @@vesion, NULL--  
4. Send the request  

## ✅ Result
The database version information is displayed on the page, confirming that the backend database is MySQL or Microsoft SQL Server.

## 🧠 Key Learning
SQL Injection can be used not only to bypass authentication but also to extract sensitive information such as database type and version.

## 🛡️ Prevention
- Use parameterized queries (prepared statements)  
- Implement proper input validation  
- Avoid exposing database errors and sensitive data  

---

## 📸 Screenshots

<img width="1347" height="676" alt="LAB4_0" src="https://github.com/user-attachments/assets/a96378c1-1e82-4e2c-9f7f-d0701ed3087f" />

**Figure 1: Normal product category request**

<br><br>
<img width="1347" height="653" alt="LAB4_1" src="https://github.com/user-attachments/assets/99d0f279-63f2-40a8-890f-f2c4721c9dc6" />

**Figure 2: Injecting ORDER BY SQL payload to determine number of the columns**

<br><br>
<img width="1353" height="658" alt="LAB4_2" src="https://github.com/user-attachments/assets/8caa5393-0e33-45fc-bbef-0f35fd014dec" />

**Figure 3: Injecting UNION based SQL payload to determine datatype of the columns**

<br><br>

<img width="1354" height="669" alt="LAB4_3" src="https://github.com/user-attachments/assets/cabaf0aa-2816-465c-9a35-836ef4b03c7d" />

**Figure 4: Displayed the version by injecting payload ' UNION SELECT @@version, NULL--**

<br><br>

<img width="1349" height="670" alt="LAB4_4" src="https://github.com/user-attachments/assets/685cc9b2-6160-4fa7-a2ce-677eecafab30" />

**Figure 5: Successful extraction of database type and version Lab Solved**
