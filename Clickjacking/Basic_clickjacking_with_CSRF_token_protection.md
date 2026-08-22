# Basic clickjacking with CSRF token protection

### Goal -

Exploit a basic clickjacking vulnerability where the page has CSRF token protection but no frame-busting.

### Vulnerability / Concept

The application has CSRF tokens but does not implement `X-Frame-Options` or `frame-ancestors` CSP, allowing the page to be embedded in an iframe. An attacker can overlay a transparent iframe to trick users into clicking.

### Exploitation

1. Verify the target page can be framed (no X-Frame-Options header)
2. Create an HTML page with a transparent iframe pointing to the target
3. Overlay deceptive UI elements to trick the user into clicking
4. The user's click triggers an action on the target page

### Why It Works

CSRF tokens protect against cross-site request forgery but not against clickjacking. Without frame-busting, the attacker can embed the target page in an iframe and use CSS transparency to overlay deceptive elements. The user's click is captured by the framed page.

### Key Takeaways

- Set `X-Frame-Options: DENY` or `SAMEORIGIN`
- Use `frame-ancestors` in CSP
- CSRF tokens do not prevent clickjacking
- Implement both CSRF and clickjacking protections
