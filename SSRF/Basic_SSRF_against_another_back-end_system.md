# Basic SSRF against another back-end system

### Goal -

Solve the PortSwigger lab: Basic SSRF against another back-end system


### Vulnerability / Concept

This lab demonstrates a vulnerability in the ssrf category.

This lab has a stock check feature which fetches data from an internal system.

The vulnerability exists because the application fails to properly validate, sanitize, or secure the user-controlled input that reaches a sensitive operation. The specific attack surface and exploitation technique depend on the exact vulnerability type demonstrated in this lab.

### Recon / Initial Analysis

Based on the lab's objective and the PortSwigger solution:

1. Analyze the application's functionality to identify the attack surface
2. Visit a product, click Check stock, intercept the request in Burp Suite, and send it to Burp Intruder.
                    
                    
                        Change the stockApi parameter t
3. Use Burp Suite Proxy to intercept and analyze requests
4. Identify the specific vulnerability type by testing user-controlled input
5. Determine the appropriate exploitation technique for this lab

### Exploitation

1. Identify the SSRF injection point
2. Test internal network access via the injection point
3. Bypass any input filters using techniques like URL encoding, DNS rebinding, or open redirects
4. Access sensitive internal endpoints or cloud metadata

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab has a stock check feature which fetches data from an internal system."

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

An attacker could access internal admin panels, steal cloud credentials from metadata endpoints (AWS IAM, GCP), scan the internal network, access databases bound to localhost, or exfiltrate data via blind SSRF.

### Detection / Testing Methodology

1. Identify parameters that accept URLs or hostnames
2. Test with http://localhost/ or http://127.0.0.1/
3. Check for input filters (blacklists, whitelists)
4. Test cloud metadata endpoints (169.254.169.254)
5. For blind SSRF: use Burp Collaborator
6. Test URL scheme bypasses (gopher://, file://)
7. Check for open redirect vulnerabilities that chain with SSRF

### Remediation

- Use allowlists (not blocklists) for URL validation
- Block all private IP ranges (10.x, 172.16-31.x, 192.168.x, 127.x, 169.254.x)
- Disable unnecessary URL schemes (file://, gopher://, dict://)
- Do not follow redirects when making server-side requests
- Use a separate network namespace for outbound requests
- Implement DNS pinning to prevent DNS rebinding

### Key Takeaways

- This lab demonstrates a ssrf vulnerability in a real-world scenario.
- The vulnerability occurs because user input reaches a sensitive operation without proper validation.
- The PortSwigger lab confirms: "This lab has a stock check feature which fetches data from an internal system."
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Use allowlists (not blocklists) for URL validation
