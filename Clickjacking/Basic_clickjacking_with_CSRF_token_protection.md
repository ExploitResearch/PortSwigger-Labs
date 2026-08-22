# Basic clickjacking with CSRF token protection

**Lab URL:** https://portswigger.net/web-security/clickjacking/lab-basic-csrf-protected

### Goal -

Exploit a basic clickjacking vulnerability where the page has CSRF token protection but no frame-busting.

### Exploitation

1. Verify the target page can be framed (no X-Frame-Options header)
2. Create an HTML page with a transparent iframe pointing to the target
3. Overlay deceptive UI elements to trick the user into clicking
4. The user's click triggers an action on the target page

### Why It Works

This lab contains login functionality and a delete account button that is protected by a CSRF token.
