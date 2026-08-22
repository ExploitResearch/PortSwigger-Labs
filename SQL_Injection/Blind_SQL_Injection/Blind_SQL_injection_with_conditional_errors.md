# Blind SQL injection with conditional errors

### Goal -

Exploit a blind SQL injection vulnerability by triggering database errors conditionally.

### Analysis / Exploitation

1. Identify the injection point
2. Test for conditional errors using CASE/IF statements
3. Use error-based extraction to retrieve data

### Why It Works

The vulnerability exists because user input is incorporated into SQL queries without parameterization. The specific technique demonstrated in this lab involves exploit a blind sql injection vulnerability by triggering database errors condit.

### Key Takeaways

- Parameterized queries prevent SQL injection entirely.
- Blind SQL injection can be exploited without visible data via conditional responses or errors.
- WAF filters can be bypassed using encoding techniques.

## PortSwigger Lab

**Official lab:** Blind SQL injection with conditional errors

**PortSwigger:** https://portswigger.net/web-security/sql-injection/blind/lab-conditional-errors
