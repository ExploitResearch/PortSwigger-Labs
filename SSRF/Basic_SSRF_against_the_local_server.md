# Basic SSRF against the local server

### Goal -

Exploit a server-side request forgery (SSRF) vulnerability to access a restricted admin interface on the local server.

### Vulnerability / Concept

The application makes HTTP requests to a user-supplied URL. By providing `http://localhost/` or `http://127.0.0.1/`, the attacker can access internal services that are not reachable from the outside.

### Exploitation

1. Identify a parameter that accepts a URL or hostname
2. Change the URL to `http://localhost/` or `http://127.0.0.1/`
3. Identify the admin interface on the local server
4. Access the admin interface through the SSRF
5. Delete the target user to solve the lab

### Why It Works

The application trusts user input to make server-side HTTP requests. The local server has an admin interface that is only accessible from localhost. By exploiting the SSRF, the attacker can access the admin interface as if they were on the local network.

### Key Takeaways

- Validate all URLs before making server-side requests
- Block access to localhost, 127.0.0.1, and private IP ranges
- Use a network-level firewall to prevent the server from accessing internal services
- Implement URL allowlists
