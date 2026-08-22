# Bypassing flawed input filters for server-side prototype pollution

### Goal -

Solve the PortSwigger lab: Bypassing flawed input filters for server-side prototype pollution

### Vulnerability / Concept

Prototype pollution occurs when user-controlled input is merged into JavaScript objects without proper validation. By injecting `__proto__` or `constructor.prototype` properties, an attacker can add or override properties on the global Object prototype, affecting all objects that inherit from it.

### Recon / Initial Analysis

1. Identify merge/assign operations that process user input (query params, JSON bodies)
2. Test for prototype pollution by injecting `__proto__[test]=polluted`
3. Check if the polluted property appears on other objects
4. Identify gadget properties that can be exploited (innerHTML, src, href, etc.)

### Exploitation

1. Identify a merge operation that accepts user input
2. Inject a prototype pollution payload via `__proto__` or `constructor.prototype`
3. Identify a gadget property that triggers the desired behavior (XSS, privilege escalation, RCE)
4. Craft the payload to exploit the specific gadget

### Why It Works

JavaScript's prototype chain means that properties on `Object.prototype` are inherited by all objects. When a merge function copies user-controlled properties without checking for `__proto__` or `constructor`, it allows pollution of the prototype chain. This can override default values, trigger unexpected code paths, or inject malicious content.

### Key Takeaways

- Never merge user-controlled input into objects without checking for `__proto__` and `constructor`
- Use `Object.create(null)` for objects that shouldn't inherit
- Client-side: can lead to DOM XSS via gadget properties
- Server-side: can lead to RCE via child_process, require, etc.
