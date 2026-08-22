# Server-side template injection using documentation

### Goal -

Solve the PortSwigger lab: Server-side template injection using documentation

### Exploitation

1. Confirm SSTI by injecting template syntax that produces a mathematical result
2. Identify the template engine via fingerprinting payloads
3. Research the engine's documentation for dangerous functions and objects
4. Craft an exploit payload that accesses restricted objects or executes code

### Why It Works

The exploit succeeds because this lab is vulnerable to server-side template injection. to solve the lab, create a custom exploit to delete the file /.ssh/id_rsa from carlos's home directory.

The root cause is a failure in the application's security architecture specific to this server side template injection scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab is vulnerable to server-side template injection. To solve the lab, create a custom exploit "
- Never concatenate user input into template strings — use template variables.
