# Privilege escalation via server-side prototype pollution

### Goal -

Solve the PortSwigger lab: Privilege escalation via server-side prototype pollution

### Exploitation

1. Identify a merge operation that accepts user input
2. Inject a prototype pollution payload via `__proto__` or `constructor.prototype`
3. Identify a gadget property that triggers the desired behavior (XSS, privilege escalation, RCE)
4. Craft the payload to exploit the specific gadget

### Why It Works

The exploit succeeds because this lab is built on node.js and the express framework. it is vulnerable to server-side prototype pollution because it unsafely merges user-controllable input into a server-side javascript object. thi

The root cause is a failure in the application's security architecture specific to this prototype pollution scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab is built on Node.js and the Express framework. It is vulnerable to server-side prototype po"
- Reject __proto__ and constructor keys in JSON input before merging.

## PortSwigger Lab

**Official lab:** Privilege escalation via server-side prototype pollution

**PortSwigger:** https://portswigger.net/web-security/prototype-pollution/server-side/lab-privilege-escalation-via-server-side-prototype-pollution
