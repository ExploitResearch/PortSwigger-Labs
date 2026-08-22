# Routing-based SSRF

### Goal -

Solve the PortSwigger lab: Routing-based SSRF

### Exploitation

1. Identify how the application uses the Host header
2. Craft a malicious Host header that exploits the specific vulnerability
3. For password reset poisoning: set Host to attacker-controlled domain
4. For SSRF: set Host to internal IP or hostname

### Why It Works

The exploit succeeds because this lab is vulnerable to routing-based ssrf via the host header. you can exploit this to access an insecure intranet admin panel located on an internal ip address.

The official solution confirms: Send the GET / request that received a 200 response to Burp Repeater. In Burp Repeater, select the Host header value, right-click and select Insert Co

The root cause is a failure in the application's security architecture specific to this host header scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab is vulnerable to routing-based SSRF via the Host header. You can exploit this to access an "
- Validate the Host header against an allowlist of expected domains.
