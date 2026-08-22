# Reflected XSS protected by CSP, with CSP bypass

### Goal -

Perform a reflected XSS attack that bypasses a Content Security Policy by finding a script source on the CSP allowlist.

### Vulnerability / Concept

The application has a CSP that allows scripts from certain whitelisted domains. One of these domains hosts a JavaScript file or JSONP endpoint that can be used to execute arbitrary code.

### Exploitation

1. Examine the CSP header to find allowed script sources
2. Check each whitelisted domain for JSONP endpoints or Angular/JS files that evaluate expressions
3. Craft a payload that loads a script from the whitelisted domain
4. Use JSONP callback or Angular template injection to execute code

### Why It Works

The CSP allows scripts from domains that host JSONP endpoints or JavaScript libraries with expression evaluation. By loading a script from a whitelisted domain with a controlled callback parameter, the attacker can execute arbitrary JavaScript within the CSP.

### Key Takeaways

- Audit all domains on the CSP script-src allowlist
- Remove JSONP endpoints from whitelisted domains
- Use nonces or hashes instead of domain allowlists
- Consider using `strict-dynamic` in CSP
