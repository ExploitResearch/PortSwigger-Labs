# Blind XXE with out-of-band interaction via XML parameter entities

### Goal -

Solve the PortSwigger lab: Blind XXE with out-of-band interaction via XML parameter entities


### Vulnerability / Concept

This lab demonstrates a vulnerability in the xxe category.

This lab has a "Check stock" feature that parses XML input, but does not display any unexpected values, and blocks requests containing regular external entities.

The vulnerability exists because the application fails to properly validate, sanitize, or secure the user-controlled input that reaches a sensitive operation. The specific attack surface and exploitation technique depend on the exact vulnerability type demonstrated in this lab.

### Recon / Initial Analysis

Based on the lab's objective and the PortSwigger solution:

1. Analyze the application's functionality to identify the attack surface
2. Visit a product page, click "Check stock" and intercept the resulting POST request in Burp Suite Professional.
                    
                    
                        
                      
3. Use Burp Suite Proxy to intercept and analyze requests
4. Identify the specific vulnerability type by testing user-controlled input
5. Determine the appropriate exploitation technique for this lab

### Exploitation

1. Identify the XML processing point
2. Craft an XML payload with an external entity definition
3. For file read: use `<!ENTITY xxe SYSTEM "file:///etc/passwd">`
4. For SSRF: use `<!ENTITY xxe SYSTEM "http://internal-service/">`
5. For blind XXE: use parameter entities and external DTD for OOB exfiltration

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab has a "Check stock" feature that parses XML input, but does not display any unexpected values, and blocks requests containing regular external entities."

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

An attacker could read arbitrary files on the server, perform SSRF to access internal services, exfiltrate data via out-of-band channels, cause denial of service (billion laughs), or execute code if XInclude supports unsafe defaults.

### Detection / Testing Methodology

1. Identify XML input points (file uploads, SOAP endpoints, SVG uploads, Office documents)
2. Test if the XML parser processes external entities
3. For blind XXE: set up an out-of-band listener (Burp Collaborator)
4. Check for XInclude support
5. Test external entity injection: <!ENTITY xxe SYSTEM "file:///etc/passwd">
6. Test parameter entity injection for blind XXE
7. Check if uploaded files (SVG, DOCX) are processed as XML

### Remediation

- Disable external entity processing in XML parsers (DOCTYPE, external entities, parameter entities)
- Use JSON instead of XML where possible
- Validate and sanitize XML input against a strict schema
- For blind XXE: monitor for outbound DNS/HTTP connections
- Disable XInclude processing unless explicitly required
- Use a WAF that understands XXE attack patterns
- Keep XML parser libraries updated

### Key Takeaways

- This lab demonstrates a xxe vulnerability in a real-world scenario.
- The vulnerability occurs because user input reaches a sensitive operation without proper validation.
- The PortSwigger lab confirms: "This lab has a "Check stock" feature that parses XML input, but does not display any unexpected valu"
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Disable external entity processing in XML parsers (DOCTYPE, external entities, parameter entities)
