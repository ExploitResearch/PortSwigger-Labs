# Reflected XSS with event handlers and href attributes blocked

**Lab URL:** https://portswigger.net/web-security/cross-site-scripting/contexts/lab-event-handlers-and-href-attributes-blocked

### Goal -

Perform a reflected XSS attack when common event handlers and href attributes are blocked by the application's input filter.

### Exploitation

1. Test which event handlers and attributes are blocked
2. Find an unblocked event handler (e.g., onpointerenter, onanimationstart, onfocus, ontoggle)
3. Craft a payload using the unblocked handler
4. Use alternative HTML elements (e.g., `<details ontoggle=...>`, `<svg><animate onbegin=...>`)

### Why It Works

The application has a reflected XSS vulnerability in the application, which can be exploited by crafting input that bypasses the insufficient validation in place.

### Key Takeaways

- The reflected XSS vulnerability is exploitable because user input is processed without adequate validation.
