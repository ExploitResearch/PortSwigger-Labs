# SSRF via flawed request parsing

### Goal -

Solve the PortSwigger lab: SSRF via flawed request parsing

### Exploitation

1. Identify how the application uses the Host header
2. Craft a malicious Host header that exploits the specific vulnerability
3. For password reset poisoning: set Host to attacker-controlled domain
4. For SSRF: set Host to internal IP or hostname

### Why It Works

The exploit succeeds because this lab is vulnerable to routing-based ssrf due to its flawed parsing of the request's intended host. you can exploit this to access an insecure intranet admin panel located at an internal ip address

The official solution confirms: Send the GET / request that received a 200 response to Burp Repeater and study the lab's behavior. Observe that the website validates the Host header 

The root cause is a failure in the application's security architecture specific to this host header scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab is vulnerable to routing-based SSRF due to its flawed parsing of the request's intended hos"
- Validate the Host header against an allowlist of expected domains.
