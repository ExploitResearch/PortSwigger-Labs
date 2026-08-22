# Password reset poisoning via dangling markup

### Goal -

Solve the PortSwigger lab: Password reset poisoning via dangling markup

### Exploitation

1. Identify how the application uses the Host header
2. Craft a malicious Host header that exploits the specific vulnerability
3. For password reset poisoning: set Host to attacker-controlled domain
4. For SSRF: set Host to internal IP or hostname

## PortSwigger Lab

**Official lab:** Password reset poisoning via dangling markup

**PortSwigger:** https://portswigger.net/web-security/host-header/exploiting/password-reset-poisoning/lab-host-header-password-reset-poisoning-via-dangling-markup
