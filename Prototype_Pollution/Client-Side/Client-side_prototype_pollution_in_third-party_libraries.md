# Client-side prototype pollution in third-party libraries

### Goal -

Solve the PortSwigger lab: Client-side prototype pollution in third-party libraries

### Exploitation

1. Identify a merge operation that accepts user input
2. Inject a prototype pollution payload via `__proto__` or `constructor.prototype`
3. Identify a gadget property that triggers the desired behavior (XSS, privilege escalation, RCE)
4. Craft the payload to exploit the specific gadget
