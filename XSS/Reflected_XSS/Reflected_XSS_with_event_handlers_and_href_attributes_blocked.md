# Reflected XSS with event handlers and href attributes blocked

### Goal -

Perform a reflected XSS attack when common event handlers and href attributes are blocked by the application's input filter.

### Vulnerability / Concept

The application blocks common XSS event handlers (onclick, onerror, onload) and href attributes, but may not block all of them. Alternative event handlers or attributes may still work.

### Exploitation

1. Test which event handlers and attributes are blocked
2. Find an unblocked event handler (e.g., onpointerenter, onanimationstart, onfocus, ontoggle)
3. Craft a payload using the unblocked handler
4. Use alternative HTML elements (e.g., `<details ontoggle=...>`, `<svg><animate onbegin=...>`)

### Why It Works

The application uses a blocklist approach that only filters common event handlers and attributes. Less common but equally dangerous handlers like `onpointerenter`, `onanimationstart`, `ontoggle`, or `onbeforetoggle` are not filtered.

### Key Takeaways

- Use allowlists, not blocklists, for input filtering
- New HTML5 event handlers are constantly being added
- Test all event handler patterns systematically
- Consider using a WAF in addition to input validation
