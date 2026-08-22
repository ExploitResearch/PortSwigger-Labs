# Host validation bypass via connection state attack

**Lab URL:** https://portswigger.net/web-security/host-header/exploiting/lab-host-header-host-validation-bypass-via-connection-state-attack

### Goal -

Solve the PortSwigger lab: Host validation bypass via connection state attack

### Exploitation

1. Identify how the application uses the Host header
2. Craft a malicious Host header that exploits the specific vulnerability
3. For password reset poisoning: set Host to attacker-controlled domain
4. For SSRF: set Host to internal IP or hostname

### Why It Works

This lab is vulnerable to routing-based SSRF via the Host header.

### Key Takeaways

- This lab is vulnerable to routing-based SSRF via the Host header.
