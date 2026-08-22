# Basic password reset poisoning

### Goal -

Solve the PortSwigger lab: Basic password reset poisoning

### Exploitation

1. Identify how the application uses the Host header
2. Craft a malicious Host header that exploits the specific vulnerability
3. For password reset poisoning: set Host to attacker-controlled domain
4. For SSRF: set Host to internal IP or hostname

## PortSwigger Lab

**Official lab:** Basic password reset poisoning

**PortSwigger:** https://portswigger.net/web-security/host-header/exploiting/password-reset-poisoning/lab-host-header-basic-password-reset-poisoning
