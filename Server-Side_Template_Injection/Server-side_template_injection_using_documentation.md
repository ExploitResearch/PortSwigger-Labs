# Server-side template injection using documentation

**Lab URL:** https://portswigger.net/web-security/server-side-template-injection/exploiting/lab-server-side-template-injection-using-documentation

### Goal -

Solve the PortSwigger lab: Server-side template injection using documentation

### Exploitation

1. Confirm SSTI by injecting template syntax that produces a mathematical result
2. Identify the template engine via fingerprinting payloads
3. Research the engine's documentation for dangerous functions and objects
4. Craft an exploit payload that accesses restricted objects or executes code

### Why It Works

This lab is vulnerable to server-side template injection.

### Key Takeaways

- This lab demonstrates using the documentation to work out how to execute arbitrary code, then delete the morale.
