# Host validation bypass via connection state attack

### Goal -

Solve the PortSwigger lab: Host validation bypass via connection state attack

### Exploitation

1. Identify how the application uses the Host header
2. Craft a malicious Host header that exploits the specific vulnerability
3. For password reset poisoning: set Host to attacker-controlled domain
4. For SSRF: set Host to internal IP or hostname

### Why It Works

The exploit succeeds because this lab is vulnerable to routing-based ssrf via the host header. although the front-end server may initially appear to perform robust validation of the host header, it makes assumptions about all req

The official solution confirms: Send the GET / request to Burp Repeater. Make the following adjustments:

The root cause is a failure in the application's security architecture specific to this host header scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab is vulnerable to routing-based SSRF via the Host header. Although the front-end server may "
- Validate the Host header against an allowlist of expected domains.
