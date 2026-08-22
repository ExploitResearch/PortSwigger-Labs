# DOM XSS via an alternative prototype pollution vector

### Goal -

Solve the PortSwigger lab: DOM XSS via an alternative prototype pollution vector


### Vulnerability / Concept

This lab demonstrates a vulnerability in the prototype pollution category.

This lab is vulnerable to DOM XSS via client-side prototype pollution. To solve the lab:

The vulnerability exists because the application fails to properly validate, sanitize, or secure the user-controlled input that reaches a sensitive operation. The specific attack surface and exploitation technique depend on the exact vulnerability type demonstrated in this lab.

### Recon / Initial Analysis

Based on the lab's objective and the PortSwigger solution:

1. Analyze the application's functionality to identify the attack surface
2. Find a prototype pollution source
                
                
                    
                        
                            In your browser, try polluting Object.prototype by injecti
3. Use Burp Suite Proxy to intercept and analyze requests
4. Identify the specific vulnerability type by testing user-controlled input
5. Determine the appropriate exploitation technique for this lab

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

The PortSwigger lab description confirms this: "This lab is vulnerable to DOM XSS via client-side prototype pollution. To solve the lab:"

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
- The PortSwigger lab confirms: "This lab is vulnerable to DOM XSS via client-side prototype pollution. To solve the lab:"
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Never merge user-controlled input into objects without checking for __proto__ and constructor
