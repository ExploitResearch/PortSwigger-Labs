# SSRF via flawed request parsing

**Lab URL:** https://portswigger.net/web-security/host-header/exploiting/lab-host-header-ssrf-via-flawed-request-parsing

### Goal -

Solve the PortSwigger lab: SSRF via flawed request parsing

### Exploitation

1. Identify how the application uses the Host header
2. Craft a malicious Host header that exploits the specific vulnerability
3. For password reset poisoning: set Host to attacker-controlled domain
4. For SSRF: set Host to internal IP or hostname

### Why It Works

This lab is vulnerable to routing-based SSRF due to its flawed parsing of the request's intended host.

### Key Takeaways

- This lab is vulnerable to routing-based SSRF due to its flawed parsing of the request's intended host.
