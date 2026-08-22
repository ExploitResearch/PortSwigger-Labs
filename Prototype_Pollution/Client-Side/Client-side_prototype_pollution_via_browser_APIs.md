# Client-side prototype pollution via browser APIs

### Goal -

Solve the PortSwigger lab: Client-side prototype pollution via browser APIs

### Exploitation

1. Identify a merge operation that accepts user input
2. Inject a prototype pollution payload via `__proto__` or `constructor.prototype`
3. Identify a gadget property that triggers the desired behavior (XSS, privilege escalation, RCE)
4. Craft the payload to exploit the specific gadget

## PortSwigger Lab

**Official lab:** Client-side prototype pollution via browser APIs

**PortSwigger:** https://portswigger.net/web-security/prototype-pollution/client-side/browser-apis/lab-prototype-pollution-client-side-prototype-pollution-via-browser-apis
