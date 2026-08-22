# Blind SQL injection with conditional errors

**Lab URL:** https://portswigger.net/web-security/sql-injection/blind/lab-conditional-errors

### Goal -

Exploit a blind SQL injection vulnerability by triggering database errors conditionally.

### Analysis / Exploitation

1. Identify the injection point
2. Test for conditional errors using CASE/IF statements
3. Use error-based extraction to retrieve data

### Why It Works

The application has a blind SQL injection vulnerability in the application, which can be exploited by crafting input that bypasses the insufficient validation in place.

### Key Takeaways

- The blind SQL injection vulnerability is exploitable because user input is processed without adequate validation.
