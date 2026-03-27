## 🔐Lab 3: SQL Injection (Oracle DB Version Enumeration)

## 🧩 Objective
To display the database type and version string.

## 🔍 Vulnerability
The application is vulnerable to SQL Injection in the product category parameter, 
allowing attackers to execute arbitrary SQL queries.

## ⚙️ Payload Used
' ORDER BY 3--
' UNION SELECT 'a', 'a' FROM DUAL--
' UNION SELECT banner, NULL FROM v$version--

## 🔎 Analysis
1. Determine the number of columns using first payload. 3 - 1= 2
2. Determine the data types of the columns using second payload
3. Output the version of the database. 

## 🚀 Steps to Reproduce
1. Navigate to the product category page
2. Intercept the request using burp suite
3. To repeater and modify the parameter: 
' UNION SELECT banner, NULL FROM v$version--
4. send the request.

## ✅ Result
The database cersion information is displayed on the page, confirming that the backend database
is oracle.

## 🧠 Key Learning
SQL injection can be used not only to bypass authentication but also to extract sensitive information such as 
database type and version.

🛡️ Prevention
Use parameterized queries (prepared statements)
Implement proper input validation
Avoid exposing database errors and sensitive data


##  📸 Screenshots
<br><br>
<img width="1305" height="669" alt="LAB3_1" src="https://github.com/user-attachments/assets/263b89d8-360d-48df-8a10-a63ffaffd8f6" />
<br><br>

**Figure 1: Normal product category request**

<br><br>
<img width="1322" height="619" alt="LAB3_2" src="https://github.com/user-attachments/assets/132ca4bd-e8ed-4b48-abf8-cbd301f90eb9" />
<br><br>

**Figure 2: Injecting ORDER BY SQL payload to determine number of the columns**

<br><br>
<img width="1347" height="643" alt="LAB3_3" src="https://github.com/user-attachments/assets/8a53e0ac-a86f-4d71-a452-1ae1528ed095" />
<br><br>

**Figure 3: Injecting UNION based SQL payload to determine datatype of the columns**

<br><br>
<img width="1333" height="641" alt="LAB3_4" src="https://github.com/user-attachments/assets/c01dcff5-8a30-46f6-a13d-3f17bb2e70f7" />
<br><br>

**Figure 4: Database version information retrieved from Oracle v$version table**

<br><br>
<img width="1355" height="662" alt="LAB3_5" src="https://github.com/user-attachments/assets/32c2c337-efd8-4097-846a-bbf10d1a10d6" />
<br><br>

**Figure 5: Successful extraction of database type and version**

<br><br>
