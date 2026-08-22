# Reflected XSS protected by CSP, with CSP bypass

### Goal -

Perform a reflected XSS attack that bypasses a Content Security Policy by finding a script source on the CSP allowlist.



### Vulnerability / Concept

This lab demonstrates a vulnerability in the cross site scripting category.

This lab uses CSP and contains a reflected XSS vulnerability.

The vulnerability exists because the application fails to properly validate, sanitize, or secure the user-controlled input that reaches a sensitive operation. The specific attack surface and exploitation technique depend on the exact vulnerability type demonstrated in this lab.

### Recon / Initial Analysis

Based on the lab's objective and the PortSwigger solution:

1. Analyze the application's functionality to identify the attack surface
2. Enter the following into the search box:
                        
                        &lt;img src=1 onerror=alert(1)&gt;
                    
                    
                        Observe t
3. Use Burp Suite Proxy to intercept and analyze requests
4. Identify the specific vulnerability type by testing user-controlled input
5. Determine the appropriate exploitation technique for this lab

### Exploitation

1. Examine the CSP header to find allowed script sources
2. Check each whitelisted domain for JSONP endpoints or Angular/JS files that evaluate expressions
3. Craft a payload that loads a script from the whitelisted domain
4. Use JSONP callback or Angular template injection to execute code

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab uses CSP and contains a reflected XSS vulnerability."

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

An attacker could steal session cookies, capture keystrokes (passwords, credit cards), perform actions on behalf of the victim, redirect users to phishing pages, deliver malware, or bypass CSRF protections.

### Detection / Testing Methodology

1. Identify input points reflected in the HTML response
2. Submit a unique marker (e.g., xssmarker123) to find exact reflection points
3. Determine the context: HTML body, attribute, JavaScript string, URL
4. Test which characters are encoded (<, >, ", ', `)
5. Test an appropriate proof-of-concept payload for the context
6. Confirm JavaScript execution
7. For DOM-based XSS: inspect JavaScript for dangerous sinks

### Remediation

- Use context-aware output encoding (HTML body, attribute, JavaScript string, URL)
- Use templating engines that auto-escape output
- Implement Content Security Policy (CSP) with script-src 'self' and nonces
- Set HttpOnly and Secure flags on session cookies
- Sanitize HTML input with allowlist-based libraries (DOMPurify)
- For DOM-based XSS: use textContent instead of innerHTML, avoid eval()

### Key Takeaways

- This lab demonstrates a cross site scripting vulnerability in a real-world scenario.
- The vulnerability occurs because user input reaches a sensitive operation without proper validation.
- The PortSwigger lab confirms: "This lab uses CSP and contains a reflected XSS vulnerability."
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Use context-aware output encoding (HTML body, attribute, JavaScript string, URL)
