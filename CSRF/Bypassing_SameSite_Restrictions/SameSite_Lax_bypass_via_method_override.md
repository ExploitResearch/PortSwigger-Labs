# SameSite Lax bypass via method override

### Goal -

Bypass SameSite=Lax cookie restrictions by using a method override technique.

### Exploitation

1. Identify that the target cookie has SameSite=Lax
2. Check if the application supports method override parameters (e.g., `_method`, `X-HTTP-Method-Override`)
3. Craft a GET request with the method override parameter set to POST
4. The server processes it as a POST while the browser sends it as a GET (bypassing SameSite=Lax)

### Why It Works

The exploit succeeds because this lab's change email function is vulnerable to csrf. to solve the lab, perform a csrf attack that changes the victim's email address. you should use the provided exploit server to host your attack.

The root cause is a failure in the application's security architecture specific to this csrf scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab's change email function is vulnerable to CSRF. To solve the lab, perform a CSRF attack that"
- CSRF tokens, SameSite cookies, and Referer validation together provide defense-in-depth.

## PortSwigger Lab

**Official lab:** SameSite Lax bypass via method override

**PortSwigger:** https://portswigger.net/web-security/csrf/bypassing-samesite-restrictions/lab-samesite-lax-bypass-via-method-override
