# Blind SSRF with out-of-band detection

### Goal -

Solve the PortSwigger lab: Blind SSRF with out-of-band detection

### Exploitation

1. Identify the SSRF injection point
2. Test internal network access via the injection point
3. Bypass any input filters using techniques like URL encoding, DNS rebinding, or open redirects
4. Access sensitive internal endpoints or cloud metadata

### Why It Works

The exploit succeeds because to solve the lab, use this functionality to cause an http request to the public burp collaborator server.

The official solution confirms: Visit a product, intercept the request in Burp Suite, and send it to Burp Repeater. Go to the Repeater tab. Select the Referer header, right-click and

The root cause is a failure in the application's security architecture specific to this ssrf scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "To solve the lab, use this functionality to cause an HTTP request to the public Burp Collaborator se"
- URL allowlists (not blocklists) and blocking private IP ranges are essential SSRF defenses.
