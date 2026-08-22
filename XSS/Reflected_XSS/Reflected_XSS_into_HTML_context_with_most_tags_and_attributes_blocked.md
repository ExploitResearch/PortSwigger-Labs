# Reflected XSS into HTML context with most tags and attributes blocked

**Lab URL:** https://portswigger.net/web-security/cross-site-scripting/contexts/lab-html-context-with-most-tags-and-attributes-blocked

### Goal -

Perform a reflected XSS attack when most HTML tags and attributes are blocked by the application's input filter.

### Exploitation

1. Test which tags are blocked (script, img, svg, etc.)
2. Find an allowed tag (e.g., `<body>`, `<style>`, `<custom-tag>`)
3. Test which event handlers are allowed on the unblocked tag
4. Craft a payload using the allowed tag and handler
5. Use Burp Intruder to fuzz for allowed tags and attributes
