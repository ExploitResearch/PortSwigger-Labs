# Reflected XSS with AngularJS sandbox escape and CSP

### Goal -

Perform an XSS attack that escapes the AngularJS sandbox AND bypasses Content Security Policy.

### Exploitation

1. Identify the AngularJS sandbox escape point
2. Examine the CSP header to find allowed script sources
3. Use the AngularJS sandbox escape with a CSP-compliant payload
4. The payload uses `window.name` or a whitelisted CDN to deliver the script

## PortSwigger Lab

**Official lab:** Reflected XSS with AngularJS sandbox escape and CSP

**PortSwigger:** https://portswigger.net/web-security/cross-site-scripting/contexts/client-side-template-injection/lab-angular-sandbox-escape-and-csp
