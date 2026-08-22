# SQL injection with filter bypass via XML encoding

### Goal -

Bypass a WAF filter that blocks SQL injection characters by using XML encoding.

### Analysis / Exploitation

1. Identify the SQL injection point that uses XML input
2. Test for character filtering (angle brackets, quotes)
3. Use XML entity encoding to bypass the filter: `&#49;` for `1`

### Why It Works

The vulnerability exists because user input is incorporated into SQL queries without parameterization. The specific technique demonstrated in this lab involves bypass a waf filter that blocks sql injection characters by using xml encoding..

### Key Takeaways

- Parameterized queries prevent SQL injection entirely.
- Blind SQL injection can be exploited without visible data via conditional responses or errors.
- WAF filters can be bypassed using encoding techniques.

## PortSwigger Lab

**Official lab:** SQL injection with filter bypass via XML encoding

**PortSwigger:** https://portswigger.net/web-security/sql-injection/lab-sql-injection-with-filter-bypass-via-xml-encoding
