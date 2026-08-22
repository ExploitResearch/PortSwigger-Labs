# Server-side pause-based request smuggling

### Goal -

Solve the PortSwigger lab: Server-side pause-based request smuggling


### Vulnerability / Concept

This lab demonstrates a vulnerability in the request smuggling category.

This lab is vulnerable to pause-based server-side request smuggling. The front-end server streams requests to the back-end, and the back-end server does not close the connection after a timeout on some endpoints.

The vulnerability exists because the application fails to properly validate, sanitize, or secure the user-controlled input that reaches a sensitive operation. The specific attack surface and exploitation technique depend on the exact vulnerability type demonstrated in this lab.

### Recon / Initial Analysis

Based on the lab's objective and the PortSwigger solution:

1. Analyze the application's functionality to identify the attack surface
2. Identify a desync vector
                
                
                    
                        
                            In Burp, notice from the Server response header that the lab is usi
3. Use Burp Suite Proxy to intercept and analyze requests
4. Identify the specific vulnerability type by testing user-controlled input
5. Determine the appropriate exploitation technique for this lab

### Exploitation

1. Identify the smuggling variant (CL.TE, TE.CL, TE.TE, H2.CL, etc.)
2. Craft a smuggled request that will be processed by the back-end server
3. The smuggled request can bypass front-end security controls, capture other users' requests, or poison the cache

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab is vulnerable to pause-based server-side request smuggling. The front-end server streams requests to the back-end, and the back-end server does not close the connection after a timeout on som"

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

An attacker could bypass front-end security controls (WAF, rate limiting), capture other users' requests (including credentials), perform web cache poisoning/deception, deliver stored XSS, or cause denial of service via response queue poisoning.

### Detection / Testing Methodology

1. Identify if the application uses a front-end/back-end architecture
2. Test for CL.TE and TE.CL vulnerabilities using timing techniques
3. Check if HTTP/2 is supported (for H2-based smuggling)
4. Identify if the front-end rewrites requests
5. Test for response queue poisoning
6. Check for client-side desync vulnerabilities

### Remediation

- Use HTTP/2 end-to-end to avoid CL/TE ambiguities
- Reject requests with both Content-Length and Transfer-Encoding headers
- Normalize HTTP/1.1 headers before forwarding
- Use strict request validation on both front-end and back-end
- Configure front-end and back-end to use the same HTTP parsing library

### Key Takeaways

- This lab demonstrates a request smuggling vulnerability in a real-world scenario.
- The vulnerability occurs because user input reaches a sensitive operation without proper validation.
- The PortSwigger lab confirms: "This lab is vulnerable to pause-based server-side request smuggling. The front-end server streams re"
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Use HTTP/2 end-to-end to avoid CL/TE ambiguities
