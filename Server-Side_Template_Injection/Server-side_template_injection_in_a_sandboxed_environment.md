# Server-side template injection in a sandboxed environment

### Goal -

Solve the PortSwigger lab: Server-side template injection in a sandboxed environment

### Exploitation

1. Confirm SSTI by injecting template syntax that produces a mathematical result
2. Identify the template engine via fingerprinting payloads
3. Research the engine's documentation for dangerous functions and objects
4. Craft an exploit payload that accesses restricted objects or executes code
