# Reflected XSS in a JavaScript URL with some characters blocked

### Goal -

Perform a reflected XSS attack via a JavaScript URL when certain characters are blocked by the application.

### Vulnerability / Concept

The application reflects user input into a `javascript:` URL but blocks certain characters. However, the blocklist is incomplete and alternative encodings or techniques can bypass it.

### Exploitation

1. Identify that input is reflected in a JavaScript URL context (href="javascript:...")
2. Test which characters are blocked (quotes, angle brackets, etc.)
3. Use alternative encoding or characters that achieve the same result
4. Craft a payload using HTML entities, Unicode, or template literals

### Why It Works

The application filters specific characters but doesn't account for alternative encodings. HTML entities, Unicode escapes, or template literals (backticks) can bypass character-based filters.

### Key Takeaways

- Character blocklists are always incomplete
- Use context-aware output encoding
- Encode based on the insertion context (URL, HTML, JavaScript)
