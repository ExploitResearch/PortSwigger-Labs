# Reflected XSS into HTML context with most tags and attributes blocked

### Goal -

Perform a reflected XSS attack when most HTML tags and attributes are blocked by the application's input filter.

### Vulnerability / Concept

The application blocks common HTML tags and event handler attributes, but the blocklist is incomplete. Some less common tags or attributes may still be allowed.

### Exploitation

1. Test which tags are blocked (script, img, svg, etc.)
2. Find an allowed tag (e.g., `<body>`, `<style>`, `<custom-tag>`)
3. Test which event handlers are allowed on the unblocked tag
4. Craft a payload using the allowed tag and handler
5. Use Burp Intruder to fuzz for allowed tags and attributes

### Why It Works

The application uses a blocklist approach to filter HTML tags and attributes. While it blocks common XSS vectors (script, img onerror, svg onload), it misses less common tags like `<body onload>`, `<style>@import`, or custom elements that can still execute JavaScript.

### Key Takeaways

- Use allowlists, not blocklists, for HTML filtering
- Test systematically for all HTML tags
- Consider using a proper HTML sanitization library
- Implement CSP as defense in depth
