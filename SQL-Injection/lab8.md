# 🔐 Lab 8: Finding a Cloumns Containing Text

## 🧩 Objective
To Identify which cloumn(s) in the SQL query can accept and display text data using a UNION-based SQL injection attack.

## 🔍 Vulnerability
The application is vulnerable to SQL Injection in the product category parameter, allowing manipulation of the SQL query.

## ⚙️ Payload Used
- ' UNION SELECT NULL, 'a'--
- ' UNION SELECT 'a', NULL--

## 🔎 Analysis
1.  Use UNION SELECT with test value('a') -> k2Hh18
2.  Inject into each columns postion one by one
3.  Observe which columns reflects the text in the response
4.  Indetify the columns that accepts string data

## 🚀 Steps to Reproduce
1. Navigate to the product category page  
2. Intercept the request using Burp Suite  
3. Send the request to Repeater  
4. Modify the parameter with:
   ' UNION SELECT 'a', NULL--  
5. Observe the response  
6. Try:
   ' UNION SELECT NULL, 'a'--  
7. Identify which column displays the value 'a'  

## ✅ Result
Successfully identified the column that accepts and displays text data.

## 🧠 Key Learning
Finding a column that supports text is essential for extracting meaningful data using UNION-based SQL Injection.

## 🛡️ Prevention
- Use parameterized queries (prepared statements)  
- Implement strict input validation  
- Avoid exposing database query results  

---

## 📸 Screenshots

<img width="1342" height="654" alt="LAB8_1" src="https://github.com/user-attachments/assets/7701aa1b-c8b5-4b04-abf1-6b3a5c531e4e" />
<br><br>

**Figure 1: Injecting UNION SELECT payload to determine number of cloumns first column**

<br><br>

<img width="1349" height="643" alt="LAB8_2" src="https://github.com/user-attachments/assets/352c6587-34ab-4f86-b944-afaf0d8dfc84" />
<br><br>

**Figure 2: Injecting UNION SELECT payload with text in second column**

<br><br>

<img width="1349" height="676" alt="LAB8_3" src="https://github.com/user-attachments/assets/11d15fb7-db37-4a53-a355-72cbb8b00120" />
<br><br>

**Figure 3: Confirming injectable text column (Lab Solved)**
