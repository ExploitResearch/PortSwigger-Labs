# DOM XSS using web messages

### Goal -

Solve the PortSwigger lab: DOM XSS using web messages



### Vulnerability / Concept

This lab demonstrates a vulnerability in the dom based category.

This lab uses web messaging and parses the message as JSON. To solve the lab, construct an HTML page on the exploit server that exploits this vulnerability and calls the print() function.

The vulnerability exists because the application fails to properly validate, sanitize, or secure the user-controlled input that reaches a sensitive operation. The specific attack surface and exploitation technique depend on the exact vulnerability type demonstrated in this lab.

### Recon / Initial Analysis

Based on the lab's objective and the PortSwigger solution:

1. Analyze the application's functionality to identify the attack surface
2. Notice that the home page contains an event listener that listens for a web message. This event listener expects a string that is parsed using JSON.parse(). In the JavaScript, we can see that the even
3. Use Burp Suite Proxy to intercept and analyze requests
4. Identify the specific vulnerability type by testing user-controlled input
5. Determine the appropriate exploitation technique for this lab

### Exploitation

1. Identify the vulnerability type and injection point
2. Craft the appropriate payload
3. Deliver the payload and verify the result

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab uses web messaging and parses the message as JSON. To solve the lab, construct an HTML page on the exploit server that exploits this vulnerability and calls the print() function."

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

An attacker could achieve DOM-based XSS via web messages, redirect users to malicious sites (open redirect), manipulate user cookies (session hijacking), bypass HTML filters via DOM clobbering, or execute JavaScript in the victim's browser context.

### Detection / Testing Methodology

1. Inspect JavaScript source for dangerous sinks (innerHTML, document.write, eval, location.href)
2. Identify sources of untrusted data (location.hash, location.search, postMessage, document.referrer)
3. Check if postMessage events validate the origin
4. Test if user-controlled data reaches DOM sinks without sanitization
5. For DOM clobbering: check if HTML elements can override JavaScript variables
6. Use DOM Invader or manual inspection to trace source-to-sink flows

### Remediation

- Validate the origin of postMessage events (event.origin check)
- Do not use user-controlled data in location.href assignments
- Sanitize data before writing to document.cookie
- Avoid using global variables that can be clobbered by HTML elements
- Use textContent instead of innerHTML
- Implement CSP with script-src 'self'

### Key Takeaways

- This lab demonstrates a dom based vulnerability in a real-world scenario.
- The vulnerability occurs because user input reaches a sensitive operation without proper validation.
- The PortSwigger lab confirms: "This lab uses web messaging and parses the message as JSON. To solve the lab, construct an HTML page"
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Validate the origin of postMessage events (event.origin check)
