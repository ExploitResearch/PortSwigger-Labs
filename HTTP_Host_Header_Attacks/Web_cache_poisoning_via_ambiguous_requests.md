# Web cache poisoning via ambiguous requests

**Lab URL:** https://portswigger.net/web-security/host-header/exploiting/lab-host-header-web-cache-poisoning-via-ambiguous-requests

### Goal -

Solve the PortSwigger lab: Web cache poisoning via ambiguous requests

### Exploitation

1. Identify how the application uses the Host header
2. Craft a malicious Host header that exploits the specific vulnerability
3. For password reset poisoning: set Host to attacker-controlled domain
4. For SSRF: set Host to internal IP or hostname

### Why It Works

This lab is vulnerable to web cache poisoning due to discrepancies in how the cache and the back-end application handle ambiguous requests.

### Key Takeaways

- This lab is vulnerable to web cache poisoning due to discrepancies in how the cache and the back-end application handle ambiguous requests.
