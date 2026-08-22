# SameSite Lax bypass via method override

### Goal -

Bypass SameSite=Lax cookie restrictions by using a method override technique.

### Vulnerability / Concept

SameSite=Lax cookies are sent with GET requests but not POST. If the application supports method override (e.g., `_method=POST` parameter), the attacker can perform a CSRF via a GET request that the server treats as a POST.

### Exploitation

1. Identify that the target cookie has SameSite=Lax
2. Check if the application supports method override parameters (e.g., `_method`, `X-HTTP-Method-Override`)
3. Craft a GET request with the method override parameter set to POST
4. The server processes it as a POST while the browser sends it as a GET (bypassing SameSite=Lax)

### Why It Works

The browser sends the cookie because the HTTP method is GET (allowed by SameSite=Lax). The server's framework interprets the method override parameter and processes the request as a POST. This mismatch allows the CSRF attack to succeed.

### Key Takeaways

- Method override features can bypass SameSite protections
- Disable method override in production
- Use SameSite=Strict for state-changing operations
- Combine SameSite with CSRF tokens
