# Basic SSRF against the local server

### Goal -

Exploit a server-side request forgery (SSRF) vulnerability to access a restricted admin interface on the local server.


### Vulnerability / Concept

Server-Side Request Forgery (SSRF) occurs when an application makes HTTP requests to a user-supplied URL without proper validation. This allows attackers to make the server send requests to unintended destinations, including internal services, cloud metadata endpoints, and localhost services.

Common SSRF targets: internal admin panels, cloud metadata endpoints (169.254.169.254), localhost services, internal network scanning, and blind SSRF via out-of-band (OOB) DNS/HTTP callbacks.

The root cause is the server trusting user input as a URL destination without validating the scheme, host, and port against an allowlist.

### Recon / Initial Analysis

1. Identify parameters that accept URLs or hostnames (image URLs, webhook URLs, import features)
2. Test with `http://localhost/` or `http://127.0.0.1/` to check internal access
3. Check for input filters (blacklists, whitelists) by testing alternative IP formats
4. Test cloud metadata endpoints (`http://169.254.169.254/latest/meta-data/`)
5. For blind SSRF: use Burp Collaborator to detect out-of-band callbacks
6. Test URL scheme bypasses (gopher://, file://, dict://)
7. Check for open redirect vulnerabilities that can be chained with SSRF

### Vulnerability / Concept

The application makes HTTP requests to a user-supplied URL. By providing `http://localhost/` or `http://127.0.0.1/`, the attacker can access internal services that are not reachable from the outside.

### Exploitation

1. Identify a parameter that accepts a URL or hostname
2. Change the URL to `http://localhost/` or `http://127.0.0.1/`
3. Identify the admin interface on the local server
4. Access the admin interface through the SSRF
5. Delete the target user to solve the lab

### Why It Works

The application makes server-side HTTP requests using user-controlled URLs without validating the destination. The server has access to internal network resources that external attackers cannot reach directly. By supplying an internal URL, the attacker uses the server as a proxy to access restricted resources.

Blacklist-based filters can be bypassed using alternative IP formats (0x7f000001, 2130706433, 017700000001), DNS rebinding, URL encoding, or redirect chains. Whitelist filters can be bypassed using open redirects on whitelisted domains.

### Real-World Impact

An attacker could:
- Access internal admin panels not exposed to the internet
- Steal cloud credentials from metadata endpoints (AWS IAM roles, GCP service accounts)
- Scan the internal network for vulnerable services
- Access databases or APIs bound to localhost
- Exfiltrate data via blind SSRF to attacker-controlled DNS/HTTP servers
- Pivot to other internal services via SSRF chains

### Remediation

- Use allowlists (not blocklists) for URL validation — only allow specific, expected domains
- Block all private IP ranges (10.x, 172.16-31.x, 192.168.x, 127.x, 169.254.x)
- Disable unnecessary URL schemes (file://, gopher://, dict://, ftp://)
- Do not follow redirects when making server-side requests
- Use a separate network namespace for outbound requests
- Implement DNS pinning to prevent DNS rebinding attacks

### Key Takeaways

- SSRF turns the server into a proxy — the server's network access becomes the attacker's.
- Cloud metadata endpoints (169.254.169.254) are high-value SSRF targets for credential theft.
- Blacklist-based URL filters are always bypassable — use allowlists.
- Open redirects on whitelisted domains can bypass URL allowlist filters.
- Blind SSRF (via OOB DNS/HTTP) can exfiltrate data even without response reflection.
