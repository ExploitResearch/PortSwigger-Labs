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

### Key Takeaways

- Always validate the Host header against an allowlist of expected domains
- Use `X-Forwarded-Host` carefully; validate it
- Password reset links should use a server-side configured base URL, not the Host header
- Reject requests with duplicate or ambiguous Host headers
