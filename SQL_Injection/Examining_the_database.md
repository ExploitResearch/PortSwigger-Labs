# Examining the database

### Goal -

Use SQL injection to examine the database structure by querying the database type and version, and listing the database contents.


### Vulnerability / Concept

SQL Injection (SQLi) occurs when user-controlled input is incorporated into SQL queries without proper parameterization. This allows attackers to manipulate the query's logic, read sensitive data, modify database contents, bypass authentication, or execute administrative operations.

Common types: UNION-based (combine query results), Boolean-based blind (infer data from true/false responses), Time-based blind (infer data from response delays), Error-based (extract data from database error messages), and Out-of-band (exfiltrate data via DNS/HTTP to attacker-controlled servers).

The root cause is always string concatenation of user input into SQL queries instead of parameterized queries (prepared statements).

### Recon / Initial Analysis

1. Identify all input points that interact with the database (search, login, product filters, URL parameters)
2. Test with single quotes (`'`), double quotes (`"`), and special SQL characters to detect syntax errors
3. Test for boolean-based blind injection (add `AND 1=1` vs `AND 1=2` and compare responses)
4. Test for time-based blind injection (add `AND SLEEP(10)` or `WAITFOR DELAY '0:0:10'`)
5. Test for UNION injection by determining column count (`ORDER BY` clause or `UNION SELECT NULL`)
6. Identify the database type (Oracle, MySQL, PostgreSQL, SQL Server) via version-specific syntax
7. Use `information_schema` or `all_tables` to enumerate database structure
8. Check if error messages are displayed (error-based injection)

### Vulnerability / Concept

The application is vulnerable to SQL injection. By examining the database structure, an attacker can identify table names, column names, and data types to craft more effective injection payloads.

### Exploitation

1. Identify the SQL injection point
2. Query the database type and version using database-specific syntax
3. List all tables in the database using `information_schema` (MySQL/PostgreSQL) or `all_tables` (Oracle)
4. List columns in the target table
5. Retrieve the data from the identified columns

### Why It Works

The application concatenates user input directly into SQL query strings instead of using parameterized queries (prepared statements). The database engine cannot distinguish between the intended query logic and the attacker's injected SQL, so it executes everything as a single query.

In blind SQLi, the application doesn't return query results or errors, but the attacker can infer data by observing differences in HTTP responses (boolean), response timing (time-based), or out-of-band network connections (OOB).

### Real-World Impact

An attacker could:
- Extract all database contents (user credentials, personal data, payment cards)
- Bypass authentication by injecting `OR 1=1` into login queries
- Modify database contents (change prices, add admin users, delete records)
- Execute OS commands via `xp_cmdshell` (SQL Server) or `COPY TO/FROM` (PostgreSQL)
- Access other databases on the same server via cross-database queries
- Cause denial of service via resource-intensive queries

### Remediation

- Use parameterized queries (prepared statements) for ALL database access — this is the primary defense
- Use stored procedures with parameterized inputs
- Implement input validation (type, length, format) as defense-in-depth
- Apply least-privilege database accounts (no `DROP`, `xp_cmdshell`, or admin access)
- Disable database error messages in production
- Use a Web Application Firewall (WAF) as additional protection

### Key Takeaways

- Parameterized queries are the only reliable defense — input validation alone is insufficient.
- Blind SQLi doesn't need visible data — boolean, time-based, and OOB techniques work without error messages.
- UNION-based injection requires knowing the column count and finding a text-type column.
- Database type matters — Oracle, MySQL, PostgreSQL, and SQL Server have different syntax and metadata tables.
- Least-privilege database accounts limit the blast radius even if injection is found.
