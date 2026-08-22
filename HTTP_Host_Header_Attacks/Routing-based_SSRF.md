# Routing-based SSRF

**Lab URL:** https://portswigger.net/web-security/host-header/exploiting/lab-host-header-routing-based-ssrf

### Goal -

Solve the PortSwigger lab: Routing-based SSRF

### Exploitation

1. Identify how the application uses the Host header
2. Craft a malicious Host header that exploits the specific vulnerability
3. For password reset poisoning: set Host to attacker-controlled domain
4. For SSRF: set Host to internal IP or hostname
