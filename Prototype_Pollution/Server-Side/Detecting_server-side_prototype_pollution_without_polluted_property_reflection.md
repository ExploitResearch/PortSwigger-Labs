# Detecting server-side prototype pollution without polluted property reflection

**Lab URL:** https://portswigger.net/web-security/prototype-pollution/server-side/lab-detecting-server-side-prototype-pollution-without-polluted-property-reflection

### Goal -

Solve the PortSwigger lab: Detecting server-side prototype pollution without polluted property reflection

### Exploitation

1. Identify a merge operation that accepts user input
2. Inject a prototype pollution payload via `__proto__` or `constructor.prototype`
3. Identify a gadget property that triggers the desired behavior (XSS, privilege escalation, RCE)
4. Craft the payload to exploit the specific gadget

### Why It Works

This lab is built on Node.

### Key Takeaways

- This lab is built on Node.
