# 🔐 Lab 14: Blind SQL Injection with Time delays

## 🧩 Objective
To exploit a Blind SQL Injection vulneraility by using time delays to extract sensitive data.

## 🔍 Vulnerability
The application is vulnerable to SQL injection, but it does not display query rsults or errors. Instead, response time differences can be infer data.

## ⚙️ Payload Used
- ' || (SELECT sleep(10))--
- ' || (SELECT pg_sleep(10))--

## 🔎 Analysis
1. Use SLEEP function to introduce delay  
2. Check the database version and perform Blind SQL injection
3. Measure response time to determine the vulnerability

## 🚀 Steps to Reproduce
1. Navigate to the vulnerable page  
2. Intercept the request using Burp Suite  
3. Send the request to Repeater  
4. Test injection:
   ' || (SELECT pg_sleep(10))--
5. Observe delayed response  
  
## ✅ Result
Successfully determine that the application is vulnerable by using sleep() function after analyzing time delay with specified time.

## 🧠 Key Learning
Time-based SQL Injection allows data extraction even when there are no visible responses or errors, by analyzing response delays.

## 🛡️ Prevention
- Use parameterized queries (prepared statements)  
- Implement strict input validation  
- Limit database query execution time  
- Monitor unusual delays in responses  

---

## 📸 Screenshots

<img width="1363" height="705" alt="LAB14_1" src="https://github.com/user-attachments/assets/06eacf2e-1031-4a6d-9f2b-60c331296742" />
<br><br>

**Figure 1: Injecting SLEEP payload causing delay**

<br><br>

<img width="1344" height="674" alt="LAB14_2" src="https://github.com/user-attachments/assets/0a00ef1c-6927-45c5-b27c-b4230092acd7" />
<br><br>

**Figure 2: Successful time-based SQL Injection (Lab Solved)**

