# Reflected XSS with event handlers and href attributes blocked

### Goal -

Perform a reflected XSS attack when common event handlers and href attributes are blocked by the application's input filter.

### Exploitation

1. Test which event handlers and attributes are blocked
2. Find an unblocked event handler (e.g., onpointerenter, onanimationstart, onfocus, ontoggle)
3. Craft a payload using the unblocked handler
4. Use alternative HTML elements (e.g., `<details ontoggle=...>`, `<svg><animate onbegin=...>`)

### Why It Works

The exploit succeeds because this lab contains a reflected xss vulnerability with some whitelisted tags, but all events and anchor href attributes are blocked.

The official solution confirms: Visit the following URL, replacing YOUR-LAB-ID with your lab ID: https://YOUR-LAB-ID.web-security-academy.net/?search=%3Csvg%3E%3Ca%3E%3Canimate+attri

The root cause is a failure in the application's security architecture specific to this cross site scripting scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- This lab contains reflected XSS vulnerability with some whitelisted tags, demonstrating how cross site scripting vulnerabilities manifest in real applications.
- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab contains a reflected XSS vulnerability with some whitelisted tags, but all events and ancho"
- Context-aware output encoding is the primary defense — the correct encoding depends on where input is reflected.

## PortSwigger Lab

**Official lab:** Reflected XSS with event handlers and href attributes blocked

**PortSwigger:** https://portswigger.net/web-security/cross-site-scripting/contexts/lab-event-handlers-and-href-attributes-blocked
