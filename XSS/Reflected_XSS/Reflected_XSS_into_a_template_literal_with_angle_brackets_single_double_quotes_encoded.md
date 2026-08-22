# Reflected XSS into a template literal with angle brackets, single, double quotes encoded

### Goal -

Perform a reflected XSS attack when the input is reflected inside a JavaScript template literal and angle brackets, single quotes, and double quotes are all encoded.

### Vulnerability / Concept

The application reflects user input inside a JavaScript template literal (backticks). While it encodes angle brackets, single quotes, and double quotes, backticks are not encoded.

### Exploitation

1. Identify that input is reflected inside backticks (template literal)
2. Test if backticks are encoded (they likely aren't)
3. Break out of the template literal using a backtick: `` `${alert(1)}` ``
4. Use the `${...}` expression syntax to execute JavaScript

### Why It Works

The application encodes characters relevant to traditional string contexts (quotes, angle brackets) but doesn't encode backticks. Since the input is inside a template literal, backticks allow breaking out and executing arbitrary expressions via `${}`.

### Key Takeaways

- Encode characters based on the actual context (template literals need backtick encoding)
- Don't assume traditional string contexts
- Use a proper output encoding library that handles all contexts
