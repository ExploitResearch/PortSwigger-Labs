# Basic SSRF against the local server

### Goal -

Exploit a server-side request forgery (SSRF) vulnerability to access a restricted admin interface on the local server.

### Exploitation

1. Identify a parameter that accepts a URL or hostname
2. Change the URL to `http://localhost/` or `http://127.0.0.1/`
3. Identify the admin interface on the local server
4. Access the admin interface through the SSRF
5. Delete the target user to solve the lab

### Why It Works

The exploit succeeds because this lab has a stock check feature which fetches data from an internal system.

The official solution confirms: Browse to /admin and observe that you can't directly access the admin page. Visit a product, click "Check stock", intercept the request in Burp Suite,

The root cause is a failure in the application's security architecture specific to this ssrf scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab has a stock check feature which fetches data from an internal system."
- URL allowlists (not blocklists) and blocking private IP ranges are essential SSRF defenses.
