# SameSite Lax bypass via method override

**Lab URL:** https://portswigger.net/web-security/csrf/bypassing-samesite-restrictions/lab-samesite-lax-bypass-via-method-override

### Goal -

Bypass SameSite=Lax cookie restrictions by using a method override technique.

### Exploitation

1. Identify that the target cookie has SameSite=Lax
2. Check if the application supports method override parameters (e.g., `_method`, `X-HTTP-Method-Override`)
3. Craft a GET request with the method override parameter set to POST
4. The server processes it as a POST while the browser sends it as a GET (bypassing SameSite=Lax)

### Why It Works

This lab's change email function is vulnerable to CSRF.

### Key Takeaways

- This lab demonstrates using the provided exploit server to host your attack.
