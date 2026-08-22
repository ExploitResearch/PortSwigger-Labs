# Host header authentication bypass

### Goal -

Solve the PortSwigger lab: Host header authentication bypass

### Exploitation

1. Identify how the application uses the Host header
2. Craft a malicious Host header that exploits the specific vulnerability
3. For password reset poisoning: set Host to attacker-controlled domain
4. For SSRF: set Host to internal IP or hostname

### Why It Works

The exploit succeeds because this lab makes an assumption about the privilege level of the user based on the http host header.

The official solution confirms: Send the GET / request that received a 200 response to Burp Repeater. Notice that you can change the Host header to an arbitrary value and still succe

The root cause is a failure in the application's security architecture specific to this host header scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab makes an assumption about the privilege level of the user based on the HTTP Host header."
- Validate the Host header against an allowlist of expected domains.

## PortSwigger Lab

**Official lab:** Host header authentication bypass

**PortSwigger:** https://portswigger.net/web-security/host-header/exploiting/lab-host-header-authentication-bypass
