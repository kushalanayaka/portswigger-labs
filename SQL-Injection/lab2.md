# 🔐 Lab 2: Authentication Bypass

## 🧩 Objective
To perform SQL injection and login as a administrator user.

## 🔍 Vulnerability
The application directly includes user input in the SQL query without proper sanitaization,
making it vulnerable to SQL injection in the authrntication process.

## ⚙️ Payload Used
' OR '1'=1-- AND '--

## 🚀 Steps to Reproduce
1.Navigate to the login page.
2. Enter the payload in username field: ' OR '1'= 1
3. Enter any value in the password field
4. Submit the login form 
5. used Burp suite and madified the request by the payload '--

## ✅ Result
Successfully logged into the application without valid credentails

## 🧠 Key Learning
SQL Injection can be used to bypasss authentication mechanisms, allowing attackers to gain
unauthorized acces to the appliaction.

##  📸 Screenshots

<img width="1176" height="606" alt="LAB2_1" src="https://github.com/user-attachments/assets/7e40854b-d911-49d0-88cf-4817ac3004e7" />
<br><br>

**Figure 1: Login page before SQL Injection attempt**


<br><br>
<img width="1245" height="603" alt="LAB2_2" src="https://github.com/user-attachments/assets/49a52daa-9eb8-4575-8ac3-a90d765f3093" />
<br><br>

**Figure 2: Injecting SQL payload (' OR 1=1--) into the username field**

<br><br>
<img width="994" height="668" alt="LAB2_7" src="https://github.com/user-attachments/assets/aea40dc1-5390-4e26-a427-0f551a6c86a3" />
<br><br>

**Figure 3: Intercepted login request in Burp Suite with injected payload**

<br><br>
<img width="1214" height="590" alt="LAB2_3" src="https://github.com/user-attachments/assets/f9fc38f6-e6ab-4ab0-ae33-cb5e7b163f58" />
<br><br>
**Figure 4: Successful authentication bypass without valid credentials**
