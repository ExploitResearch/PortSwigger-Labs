# DOM XSS via client-side prototype pollution

### Goal -

Solve the PortSwigger lab: DOM XSS via client-side prototype pollution

### Exploitation

1. Identify a merge operation that accepts user input
2. Inject a prototype pollution payload via `__proto__` or `constructor.prototype`
3. Identify a gadget property that triggers the desired behavior (XSS, privilege escalation, RCE)
4. Craft the payload to exploit the specific gadget

## PortSwigger Lab

**Official lab:** DOM XSS via client-side prototype pollution

**PortSwigger:** https://portswigger.net/web-security/prototype-pollution/client-side/lab-prototype-pollution-dom-xss-via-client-side-prototype-pollution
