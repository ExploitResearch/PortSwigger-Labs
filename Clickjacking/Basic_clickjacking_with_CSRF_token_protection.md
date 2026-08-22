# Basic clickjacking with CSRF token protection

### Goal -

Exploit a basic clickjacking vulnerability where the page has CSRF token protection but no frame-busting.

### Exploitation

1. Verify the target page can be framed (no X-Frame-Options header)
2. Create an HTML page with a transparent iframe pointing to the target
3. Overlay deceptive UI elements to trick the user into clicking
4. The user's click triggers an action on the target page

### Why It Works

The exploit succeeds because this lab contains login functionality and a delete account button that is protected by a csrf token. a user will click on elements that display the word "click" on a decoy website.

The official solution confirms: Log in to your account on the target website. Go to the exploit server and paste the following HTML template into the Body section: &lt;style&gt; ifra

The root cause is a failure in the application's security architecture specific to this clickjacking scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- This lab contains login functionality and a delete account button that is protected by a CSRF token, demonstrating how clickjacking vulnerabilities manifest in real applications.
- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab contains login functionality and a delete account button that is protected by a CSRF token."
- Set X-Frame-Options or CSP frame-ancestors — JavaScript frame-busting is bypassable.
