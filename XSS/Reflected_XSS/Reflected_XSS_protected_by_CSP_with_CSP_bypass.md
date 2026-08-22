# Reflected XSS protected by CSP, with CSP bypass

**Lab URL:** https://portswigger.net/web-security/cross-site-scripting/content-security-policy/lab-csp-bypass

### Goal -

Perform a reflected XSS attack that bypasses a Content Security Policy by finding a script source on the CSP allowlist.

### Exploitation

1. Examine the CSP header to find allowed script sources
2. Check each whitelisted domain for JSONP endpoints or Angular/JS files that evaluate expressions
3. Craft a payload that loads a script from the whitelisted domain
4. Use JSONP callback or Angular template injection to execute code

### Why It Works

The application has a reflected XSS vulnerability in the application, which can be exploited by crafting input that bypasses the insufficient validation in place.

### Key Takeaways

- The reflected XSS vulnerability is exploitable because user input is processed without adequate validation.
