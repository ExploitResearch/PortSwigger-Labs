# Host header authentication bypass

### Goal -

Solve the PortSwigger lab: Host header authentication bypass


### Vulnerability / Concept

This lab demonstrates a vulnerability in the host header category.

This lab makes an assumption about the privilege level of the user based on the HTTP Host header.

The vulnerability exists because the application fails to properly validate, sanitize, or secure the user-controlled input that reaches a sensitive operation. The specific attack surface and exploitation technique depend on the exact vulnerability type demonstrated in this lab.

### Recon / Initial Analysis

Based on the lab's objective and the PortSwigger solution:

1. Analyze the application's functionality to identify the attack surface
2. Send the GET / request that received a 200 response to Burp Repeater. Notice that you can change the Host header to an arbitrary value and still successfully access the home page.
                    
3. Use Burp Suite Proxy to intercept and analyze requests
4. Identify the specific vulnerability type by testing user-controlled input
5. Determine the appropriate exploitation technique for this lab

### Exploitation

1. Identify how the application uses the Host header
2. Craft a malicious Host header that exploits the specific vulnerability
3. For password reset poisoning: set Host to attacker-controlled domain
4. For SSRF: set Host to internal IP or hostname

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab makes an assumption about the privilege level of the user based on the HTTP Host header."

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

An attacker could hijack password reset emails (account takeover), bypass authentication via virtual host routing, perform web cache poisoning, access internal services via SSRF, or poison intermediate caches.

### Detection / Testing Methodology

1. Test if the application accepts arbitrary Host headers
2. Check if password reset emails include the Host header value
3. Test if routing is affected by Host header manipulation
4. Check for duplicate Host headers or X-Forwarded-Host support
5. Test for web cache poisoning via ambiguous Host headers
6. Check if internal services can be accessed via Host header SSRF

### Remediation

- Always validate the Host header against an allowlist of expected domains
- Use server-side configured base URLs for generating links
- Reject requests with duplicate or ambiguous Host headers
- Do not trust X-Forwarded-Host without validation
- Configure the web server to only accept expected virtual hosts
- Use absolute URLs in email templates

### Key Takeaways

- This lab demonstrates a host header vulnerability in a real-world scenario.
- The vulnerability occurs because user input reaches a sensitive operation without proper validation.
- The PortSwigger lab confirms: "This lab makes an assumption about the privilege level of the user based on the HTTP Host header."
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Always validate the Host header against an allowlist of expected domains
