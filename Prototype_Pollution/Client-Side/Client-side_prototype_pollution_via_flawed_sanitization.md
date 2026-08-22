# Client-side prototype pollution via flawed sanitization

### Goal -

Solve the PortSwigger lab: Client-side prototype pollution via flawed sanitization

### Exploitation

1. Identify a merge operation that accepts user input
2. Inject a prototype pollution payload via `__proto__` or `constructor.prototype`
3. Identify a gadget property that triggers the desired behavior (XSS, privilege escalation, RCE)
4. Craft the payload to exploit the specific gadget

### Why It Works

The exploit succeeds because this lab is vulnerable to dom xss via client-side prototype pollution. this is due to a gadget in a third-party library, which is easy to miss due to the minified source code. although it's technicall

The official solution confirms: Load the lab in Burp's built-in browser. Enable DOM Invader and enable the prototype pollution option.

The root cause is a failure in the application's security architecture specific to this prototype pollution scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab is vulnerable to DOM XSS via client-side prototype pollution. This is due to a gadget in a "
- Reject __proto__ and constructor keys in JSON input before merging.

## PortSwigger Lab

**Official lab:** Client-side prototype pollution via flawed sanitization

**PortSwigger:** https://portswigger.net/web-security/prototype-pollution/client-side/lab-prototype-pollution-client-side-prototype-pollution-via-flawed-sanitization
