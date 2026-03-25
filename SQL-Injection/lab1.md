# 🔐 Lab 1: WHERE Clause (Hidden data retrieval)

## 🧩 Objective
To retrirve hidden (unreleased) products by exploaiting a SQL injection vulnerability in the WHERE clause.

## 🔍 Vulnerability
The application directly includes user input in the SQL query without proper sanitization, making it vulnerable to SQL Injection.

## ⚙️ Payload Used
Gifts' OR 1=1--

## 🚀 Steps to Reproduce
1. Navigate to the product categaory page
2. Observe the URL parameter /filter?category=Gifts
3. Modify the category parameter to: Gift' OR 1=1--
4. Press Enter to send the request

## ✅ Result
All products are displayed, including hidden/unreleased items.

## 🧠 Key Learning
SQL Injection can manipulate query logic, allowing attackers to bypass filters and access restricted data.

### Screenshot Image Before injection.
<img width="1366" height="768" alt="Screenshot (37)" src="https://github.com/user-attachments/assets/4e07c99a-b14e-41da-b70c-d62ed1f8bfb3" />

### Screenshot Image After injection.
<img width="1245" height="665" alt="LAB1_3" src="https://github.com/user-attachments/assets/6f322876-7ab6-4569-a7b1-175607b5d293" />

<img width="1115" height="692" alt="LAB1_2" src="https://github.com/user-attachments/assets/2597408d-efaa-484f-a45c-ee841eae4411" />

