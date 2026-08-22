# Blind SQL injection with conditional responses

**Lab URL:** https://portswigger.net/web-security/sql-injection/blind/lab-conditional-responses

### Goal -

Exploit a blind SQL injection vulnerability by observing differences in the application's responses to conditional queries.

### Analysis / Exploitation

1. Identify the tracking cookie as the injection point
2. Test conditional responses: `'+AND+1=1--` vs `'+AND+1=2--`
3. Use conditional logic to extract data character by character
