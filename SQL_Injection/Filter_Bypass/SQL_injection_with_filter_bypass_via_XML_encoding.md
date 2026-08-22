# SQL injection with filter bypass via XML encoding

**Lab URL:** https://portswigger.net/web-security/sql-injection/lab-sql-injection-with-filter-bypass-via-xml-encoding

### Goal -

Bypass a WAF filter that blocks SQL injection characters by using XML encoding.

### Analysis / Exploitation

1. Identify the SQL injection point that uses XML input
2. Test for character filtering (angle brackets, quotes)
3. Use XML entity encoding to bypass the filter: `&#49;` for `1`

### Why It Works

The application has a SQL injection vulnerability in its stock check feature, which can be exploited by crafting input that bypasses the insufficient validation in place.

### Key Takeaways

- This lab demonstrates using a UNION attack to retrieve data from other tables.
- The SQL injection vulnerability is exploitable because user input is processed without adequate validation.
