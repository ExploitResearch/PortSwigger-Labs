# Reflected XSS into a JavaScript string with angle brackets and double quotes HTML-encoded and single quotes escaped

### Goal -

Perform a reflected XSS attack when angle brackets, double quotes are HTML-encoded, and single quotes are escaped with backslash.

### Vulnerability / Concept

The application encodes angle brackets and double quotes, and escapes single quotes with backslash. However, backslashes themselves are not escaped, allowing the escaping to be neutralized.

### Exploitation

1. Identify that input is reflected inside a JavaScript string with single quotes
2. Test that single quotes are escaped as `\'`
3. Inject a backslash before the escaped quote: `\\'`
4. The backslash escapes the backslash, leaving the quote unescaped
5. Break out of the string and inject JavaScript code

### Why It Works

The application escapes single quotes by prepending a backslash (`\'`). However, if the user input contains a backslash before the single quote, the backslash escapes the backslash instead of the quote, leaving the quote unescaped. This allows breaking out of the JavaScript string context.

### Key Takeaways

- Escape backslashes before escaping quotes
- Use parameterized output encoding libraries
- Don't rely on simple string replacement for escaping
- Use JSON.stringify() for JavaScript string contexts
