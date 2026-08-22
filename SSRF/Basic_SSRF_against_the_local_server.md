# Basic SSRF against the local server

**Lab URL:** https://portswigger.net/web-security/ssrf/lab-basic-ssrf-against-localhost

### Goal -

Exploit a server-side request forgery (SSRF) vulnerability to access a restricted admin interface on the local server.

### Exploitation

1. Identify a parameter that accepts a URL or hostname
2. Change the URL to `http://localhost/` or `http://127.0.0.1/`
3. Identify the admin interface on the local server
4. Access the admin interface through the SSRF
5. Delete the target user to solve the lab
