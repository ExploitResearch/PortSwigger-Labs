# Server-side template injection using documentation

### Goal -

Solve the PortSwigger lab: Server-side template injection using documentation


### Vulnerability / Concept

This lab demonstrates a vulnerability in the server side template injection category.

This lab is vulnerable to server-side template injection. To solve the lab, create a custom exploit to delete the file /.ssh/id_rsa from Carlos's home directory.

The vulnerability exists because the application fails to properly validate, sanitize, or secure the user-controlled input that reaches a sensitive operation. The specific attack surface and exploitation technique depend on the exact vulnerability type demonstrated in this lab.

### Recon / Initial Analysis

1. Analyze the application's functionality and identify user-controlled inputs
2. Use Burp Suite to intercept and modify requests
3. Test for the specific server side template injection vulnerability
4. Identify the injection point and context
5. Craft an appropriate payload

### Exploitation

1. Confirm SSTI by injecting template syntax that produces a mathematical result
2. Identify the template engine via fingerprinting payloads
3. Research the engine's documentation for dangerous functions and objects
4. Craft an exploit payload that accesses restricted objects or executes code

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab is vulnerable to server-side template injection. To solve the lab, create a custom exploit to delete the file /.ssh/id_rsa from Carlos's home directory."

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

An attacker could execute arbitrary code on the server (RCE), read sensitive files, access internal services and databases, modify or delete server-side data, or achieve full server compromise.

### Detection / Testing Methodology

1. Identify template rendering points (email templates, custom greetings, search results)
2. Test with template syntax probes: {{7*7}} (Jinja2/Twig), <%= 7*7 %> (ERB), ${7*7} (FreeMarker)
3. Identify the template engine by testing engine-specific syntax
4. Check for sandbox restrictions
5. Research the engine's documentation for dangerous functions
6. Craft an exploit that accesses restricted objects or executes code

### Remediation

- Never concatenate user input into template strings; always use template variables
- Use sandboxed template environments with restricted function access
- Implement allowlists for template functions and filters
- Use logic-less templates (Mustache) where possible
- Validate and sanitize all template input
- Run template rendering in isolated containers

### Key Takeaways

- This lab demonstrates a server side template injection vulnerability in a real-world scenario.
- The vulnerability occurs because user input reaches a sensitive operation without proper validation.
- The PortSwigger lab confirms: "This lab is vulnerable to server-side template injection. To solve the lab, create a custom exploit "
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Never concatenate user input into template strings; always use template variables
