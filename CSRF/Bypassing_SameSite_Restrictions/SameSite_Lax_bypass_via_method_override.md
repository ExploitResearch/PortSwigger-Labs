# SameSite Lax bypass via method override

### Goal -

Bypass SameSite=Lax cookie restrictions by using a method override technique.



### Vulnerability / Concept

This lab demonstrates a vulnerability in the csrf category.

This lab's change email function is vulnerable to CSRF. To solve the lab, perform a CSRF attack that changes the victim's email address. You should use the provided exploit server to host your attack.

The vulnerability exists because the application fails to properly validate, sanitize, or secure the user-controlled input that reaches a sensitive operation. The specific attack surface and exploitation technique depend on the exact vulnerability type demonstrated in this lab.

### Recon / Initial Analysis

1. Analyze the application's functionality and identify user-controlled inputs
2. Use Burp Suite to intercept and modify requests
3. Test for the specific csrf vulnerability
4. Identify the injection point and context
5. Craft an appropriate payload

### Exploitation

1. Identify that the target cookie has SameSite=Lax
2. Check if the application supports method override parameters (e.g., `_method`, `X-HTTP-Method-Override`)
3. Craft a GET request with the method override parameter set to POST
4. The server processes it as a POST while the browser sends it as a GET (bypassing SameSite=Lax)

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab's change email function is vulnerable to CSRF. To solve the lab, perform a CSRF attack that changes the victim's email address. You should use the provided exploit server to host your attack."

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

An attacker could change the victim's email address (account takeover via password reset), transfer funds, modify account settings (disable 2FA), delete data, or perform any action the victim is authorized to perform.

### Detection / Testing Methodology

1. Identify state-changing endpoints (POST/PUT/DELETE)
2. Check if the application uses CSRF tokens
3. Examine how tokens are validated (presence, session-binding, method-dependence)
4. Test if SameSite cookie attributes are set
5. Check if Referer/Origin header validation is performed
6. Attempt to submit a cross-origin form without the token

### Remediation

- Use CSRF tokens that are unique per session and validated server-side
- Implement SameSite=Strict or SameSite=Lax on session cookies
- Validate the Referer or Origin header on state-changing requests
- Require re-authentication for critical actions
- Never perform state-changing operations via GET requests

### Key Takeaways

- This lab demonstrates a csrf vulnerability in a real-world scenario.
- The vulnerability occurs because user input reaches a sensitive operation without proper validation.
- The PortSwigger lab confirms: "This lab's change email function is vulnerable to CSRF. To solve the lab, perform a CSRF attack that"
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Use CSRF tokens that are unique per session and validated server-side
