# Host header authentication bypass

**Lab URL:** https://portswigger.net/web-security/host-header/exploiting/lab-host-header-authentication-bypass

### Goal -

Solve the PortSwigger lab: Host header authentication bypass

### Exploitation

1. Identify how the application uses the Host header
2. Craft a malicious Host header that exploits the specific vulnerability
3. For password reset poisoning: set Host to attacker-controlled domain
4. For SSRF: set Host to internal IP or hostname

### Why It Works

This lab makes an assumption about the privilege level of the user based on the HTTP Host header.

### Key Takeaways

- This lab makes an assumption about the privilege level of the user based on the HTTP Host header.
