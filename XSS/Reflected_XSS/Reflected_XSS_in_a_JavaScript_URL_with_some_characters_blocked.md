# Reflected XSS in a JavaScript URL with some characters blocked

**Lab URL:** https://portswigger.net/web-security/cross-site-scripting/contexts/lab-javascript-url-some-characters-blocked

### Goal -

Perform a reflected XSS attack via a JavaScript URL when certain characters are blocked by the application.

### Exploitation

1. Identify that input is reflected in a JavaScript URL context (href="javascript:...")
2. Test which characters are blocked (quotes, angle brackets, etc.)
3. Use alternative encoding or characters that achieve the same result
4. Craft a payload using HTML entities, Unicode, or template literals
