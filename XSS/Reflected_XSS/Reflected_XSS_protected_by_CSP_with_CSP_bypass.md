# Reflected XSS protected by CSP, with CSP bypass

### Goal -

Perform a reflected XSS attack that bypasses a Content Security Policy by finding a script source on the CSP allowlist.

### Exploitation

1. Examine the CSP header to find allowed script sources
2. Check each whitelisted domain for JSONP endpoints or Angular/JS files that evaluate expressions
3. Craft a payload that loads a script from the whitelisted domain
4. Use JSONP callback or Angular template injection to execute code

### Why It Works

The exploit succeeds because this lab uses csp and contains a reflected xss vulnerability.

The official solution confirms: Enter the following into the search box: &lt;img src=1 onerror=alert(1)&gt; Observe that the payload is reflected, but the CSP prevents the script fro

The root cause is a failure in the application's security architecture specific to this cross site scripting scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- This lab contains reflected XSS vulnerability, demonstrating how cross site scripting vulnerabilities manifest in real applications.
- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab uses CSP and contains a reflected XSS vulnerability."
- Context-aware output encoding is the primary defense — the correct encoding depends on where input is reflected.
