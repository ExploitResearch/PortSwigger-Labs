# Remote code execution via server-side prototype pollution

### Goal -

Solve the PortSwigger lab: Remote code execution via server-side prototype pollution


### Vulnerability / Concept

This lab demonstrates a vulnerability in the prototype pollution category.

This lab is built on Node.js and the Express framework. It is vulnerable to server-side prototype pollution because it unsafely merges user-controllable input into a server-side JavaScript object.

The vulnerability exists because the application fails to properly validate, sanitize, or secure the user-controlled input that reaches a sensitive operation. The specific attack surface and exploitation technique depend on the exact vulnerability type demonstrated in this lab.

### Recon / Initial Analysis

1. Analyze the application's functionality and identify user-controlled inputs
2. Use Burp Suite to intercept and modify requests
3. Test for the specific prototype pollution vulnerability
4. Identify the injection point and context
5. Craft an appropriate payload

### Exploitation

1. Identify a merge operation that accepts user input
2. Inject a prototype pollution payload via `__proto__` or `constructor.prototype`
3. Identify a gadget property that triggers the desired behavior (XSS, privilege escalation, RCE)
4. Craft the payload to exploit the specific gadget

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab is built on Node.js and the Express framework. It is vulnerable to server-side prototype pollution because it unsafely merges user-controllable input into a server-side JavaScript object."

### Attack Flow

**Attack Flow:**

```
Attacker Input (payload in request)
        ↓
Application Functionality (processes user input)
        ↓
Server Processing (no validation/sanitization)
        ↓
Injection Point (input reaches sensitive operation)
        ↓
Exploitation (payload executes as intended)
        ↓
Lab Objective Achieved
```

### Real-World Impact

An attacker could achieve DOM-based XSS by polluting gadget properties, escalate privileges by overriding isAdmin/role properties, execute arbitrary code on the server (RCE) via child_process gadgets, or exfiltrate sensitive data.

### Detection / Testing Methodology

1. Identify merge/assign operations that process user input
2. Test for prototype pollution via __proto__[test]=polluted
3. Check if the polluted property appears on other objects
4. Identify gadget properties (innerHTML, src, href, etc.)
5. For server-side: test with JSON payloads containing __proto__
6. Check if the application uses vulnerable third-party libraries

### Remediation

- Never merge user-controlled input into objects without checking for __proto__ and constructor
- Use Object.create(null) for objects that should not inherit a prototype
- Use Map instead of plain objects for user-controlled key-value pairs
- Implement input validation that rejects __proto__, constructor, and prototype keys
- Use JSON.parse() with a reviver function
- Keep dependencies updated

### Key Takeaways

- This lab demonstrates a prototype pollution vulnerability in a real-world scenario.
- The vulnerability occurs because user input reaches a sensitive operation without proper validation.
- The PortSwigger lab confirms: "This lab is built on Node.js and the Express framework. It is vulnerable to server-side prototype po"
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Never merge user-controlled input into objects without checking for __proto__ and constructor
