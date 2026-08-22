# Blind SSRF with out-of-band detection

**Lab URL:** https://portswigger.net/web-security/ssrf/blind/lab-out-of-band-detection

### Goal -

Solve the PortSwigger lab: Blind SSRF with out-of-band detection

### Exploitation

1. Identify the SSRF injection point
2. Test internal network access via the injection point
3. Bypass any input filters using techniques like URL encoding, DNS rebinding, or open redirects
4. Access sensitive internal endpoints or cloud metadata

### Why It Works

To solve the lab, use this functionality to cause an HTTP request to the public Burp Collaborator server.

### Key Takeaways

- This lab demonstrates using this functionality to cause an HTTP request to the public Burp Collaborator server.
