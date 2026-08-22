# Host header authentication bypass

### Goal -

Solve the PortSwigger lab: Host header authentication bypass

### Vulnerability / Concept

HTTP Host header attacks exploit applications that use the `Host` header for security-sensitive operations without validating it. This can lead to password reset poisoning, authentication bypass, SSRF, or cache poisoning.

### Recon / Initial Analysis

1. Test if the application accepts arbitrary Host headers
2. Check if password reset emails include the Host header value
3. Test if routing is affected by Host header manipulation
4. Check for duplicate Host headers or X-Forwarded-Host support

### Exploitation

1. Identify how the application uses the Host header
2. Craft a malicious Host header that exploits the specific vulnerability
3. For password reset poisoning: set Host to attacker-controlled domain
4. For SSRF: set Host to internal IP or hostname

### Why It Works

The application trusts the `Host` header to determine the server's own hostname, which it uses for generating links, routing, and authentication. Without validation, an attacker can supply a malicious Host value that causes the application to generate links pointing to attacker-controlled domains.


### Real-World Impact

An attacker could:
- Hijack password reset emails by poisoning the Host header (account takeover)
- Bypass authentication by manipulating virtual host routing
- Perform web cache poisoning via ambiguous Host headers
- Access internal services via SSRF through Host header manipulation
- Poison intermediate caches to serve malicious content to other users
- Bypass access controls that rely on the Host header for routing


### Remediation

- Always validate the Host header against an allowlist of expected domains
- Use server-side configured base URLs for generating links (password reset, email verification)
- Reject requests with duplicate or ambiguous Host headers
- Do not trust X-Forwarded-Host without validation
- Configure the web server to only accept requests for expected virtual hosts
- Use absolute URLs in email templates instead of constructing from Host header
- Implement HSTS to prevent protocol downgrade attacks

### Key Takeaways

- Always validate the Host header against an allowlist of expected domains
- Use `X-Forwarded-Host` carefully; validate it
- Password reset links should use a server-side configured base URL, not the Host header
- Reject requests with duplicate or ambiguous Host headers
