# DOM-based open redirection

**Lab URL:** https://portswigger.net/web-security/dom-based/open-redirection/lab-dom-open-redirection

### Goal -

Solve the PortSwigger lab: DOM-based open redirection

### Exploitation

1. Identify the vulnerability type and injection point
2. Craft the appropriate payload
3. Deliver the payload and verify the result

### Why It Works

The application has a DOM-based open-redirection vulnerability in the application, which can be exploited by crafting input that bypasses the insufficient validation in place.

### Key Takeaways

- The DOM-based open-redirection vulnerability is exploitable because user input is processed without adequate validation.
