# Web cache poisoning via ambiguous requests

### Goal -

Solve the PortSwigger lab: Web cache poisoning via ambiguous requests

### Exploitation

1. Identify how the application uses the Host header
2. Craft a malicious Host header that exploits the specific vulnerability
3. For password reset poisoning: set Host to attacker-controlled domain
4. For SSRF: set Host to internal IP or hostname

### Why It Works

The exploit succeeds because this lab is vulnerable to web cache poisoning due to discrepancies in how the cache and the back-end application handle ambiguous requests. an unsuspecting user regularly visits the site's home page.

The official solution confirms: In Burp's browser, open the lab and click Home to refresh the home page. In Proxy &gt; HTTP history, right-click the GET / request and select Send to 

The root cause is a failure in the application's security architecture specific to this host header scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab is vulnerable to web cache poisoning due to discrepancies in how the cache and the back-end"
- Validate the Host header against an allowlist of expected domains.

## PortSwigger Lab

**Official lab:** Web cache poisoning via ambiguous requests

**PortSwigger:** https://portswigger.net/web-security/host-header/exploiting/lab-host-header-web-cache-poisoning-via-ambiguous-requests
