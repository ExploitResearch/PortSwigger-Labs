# SQL injection with filter bypass via XML encoding

**Lab URL:** https://portswigger.net/web-security/sql-injection/lab-sql-injection-with-filter-bypass-via-xml-encoding

### Goal -

Bypass a WAF filter that blocks SQL injection characters by using XML encoding.

### Analysis / Exploitation

1. Identify the SQL injection point that uses XML input
2. Test for character filtering (angle brackets, quotes)
3. Use XML entity encoding to bypass the filter: `&#49;` for `1`
