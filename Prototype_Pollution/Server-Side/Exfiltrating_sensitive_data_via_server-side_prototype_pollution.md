# Exfiltrating sensitive data via server-side prototype pollution

**Lab URL:** https://portswigger.net/web-security/prototype-pollution/server-side/lab-exfiltrating-sensitive-data-via-server-side-prototype-pollution

### Goal -

Solve the PortSwigger lab: Exfiltrating sensitive data via server-side prototype pollution

### Exploitation

1. Identify a merge operation that accepts user input
2. Inject a prototype pollution payload via `__proto__` or `constructor.prototype`
3. Identify a gadget property that triggers the desired behavior (XSS, privilege escalation, RCE)
4. Craft the payload to exploit the specific gadget
