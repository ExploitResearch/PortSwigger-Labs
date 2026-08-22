# DOM XSS via an alternative prototype pollution vector

### Goal -

Solve the PortSwigger lab: DOM XSS via an alternative prototype pollution vector

### Exploitation

1. Identify a merge operation that accepts user input
2. Inject a prototype pollution payload via `__proto__` or `constructor.prototype`
3. Identify a gadget property that triggers the desired behavior (XSS, privilege escalation, RCE)
4. Craft the payload to exploit the specific gadget

### Why It Works

The exploit succeeds because this lab is vulnerable to dom xss via client-side prototype pollution. to solve the lab:

The official solution confirms: Find a prototype pollution source In your browser, try polluting Object.prototype by injecting an arbitrary property via the query string: /?__

The root cause is a failure in the application's security architecture specific to this prototype pollution scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab is vulnerable to DOM XSS via client-side prototype pollution. To solve the lab:"
- Reject __proto__ and constructor keys in JSON input before merging.
