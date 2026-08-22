# Blind SQL injection with conditional responses

### Goal -

Exploit a blind SQL injection vulnerability by observing differences in the application's responses to conditional queries.

### Analysis / Exploitation

1. Identify the tracking cookie as the injection point
2. Test conditional responses: `'+AND+1=1--` vs `'+AND+1=2--`
3. Use conditional logic to extract data character by character

### Why It Works

The vulnerability exists because user input is incorporated into SQL queries without parameterization. The specific technique demonstrated in this lab involves exploit a blind sql injection vulnerability by observing differences in the appl.

### Key Takeaways

- Parameterized queries prevent SQL injection entirely.
- Blind SQL injection can be exploited without visible data via conditional responses or errors.
- WAF filters can be bypassed using encoding techniques.

## PortSwigger Lab

**Official lab:** Blind SQL injection with conditional responses

**PortSwigger:** https://portswigger.net/web-security/sql-injection/blind/lab-conditional-responses
