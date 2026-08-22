# Reflected XSS with AngularJS sandbox escape and CSP

### Goal -

Perform an XSS attack that escapes the AngularJS sandbox AND bypasses Content Security Policy.

### Vulnerability / Concept

The application uses AngularJS with a sandbox and has a CSP that blocks inline scripts. The CSP allows scripts from a whitelisted domain. The AngularJS sandbox escape can be combined with a CSP bypass.

### Exploitation

1. Identify the AngularJS sandbox escape point
2. Examine the CSP header to find allowed script sources
3. Use the AngularJS sandbox escape with a CSP-compliant payload
4. The payload uses `window.name` or a whitelisted CDN to deliver the script

### Why It Works

AngularJS expressions execute even with CSP because they are evaluated by Angular's own parser, not by `eval()`. The CSP can be bypassed by using Angular's own template evaluation or by finding a script source on the CSP allowlist.

### Key Takeaways

- CSP alone cannot prevent AngularJS sandbox escapes
- Angular expressions are executed by the framework, bypassing CSP
- Combine CSP with input sanitization
- Upgrade Angular versions
