# Discovering vulnerabilities quickly with targeted scanning

### Goal -

Solve the PortSwigger lab: Discovering vulnerabilities quickly with targeted scanning


### Vulnerability / Concept

This lab demonstrates a vulnerability in the essential skills category.

This lab contains a vulnerability that enables you to read arbitrary files from the server. To solve the lab, retrieve the contents of /etc/passwd within 10 minutes.

The vulnerability exists because the application fails to properly validate, sanitize, or secure the user-controlled input that reaches a sensitive operation. The specific attack surface and exploitation technique depend on the exact vulnerability type demonstrated in this lab.

### Recon / Initial Analysis

Based on the lab's objective and the PortSwigger solution:

1. Analyze the application's functionality to identify the attack surface
2. This lab is designed to help you learn how targeted scans can assist you with basic recon. As such, we will not be providing a step-by-step solution.
3. Use Burp Suite Proxy to intercept and analyze requests
4. Identify the specific vulnerability type by testing user-controlled input
5. Determine the appropriate exploitation technique for this lab

### Exploitation

1. Configure Burp Scanner for the target data structure
2. Run targeted scans on identified insertion points
3. Analyze scanner findings and verify manually

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab contains a vulnerability that enables you to read arbitrary files from the server. To solve the lab, retrieve the contents of /etc/passwd within 10 minutes."

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

Proper use of Burp Suite Scanner enables rapid identification of vulnerabilities across large attack surfaces, detection of non-standard data structure vulnerabilities, more efficient manual testing, and better coverage.

### Detection / Testing Methodology

1. Configure Burp Scanner with appropriate insertion point types
2. Set up crawl-and-scan workflows
3. Use targeted scanning for specific data structures
4. Analyze scanner findings and verify manually
5. Use Burp's extension ecosystem for specialized testing

### Remediation

- Configure Burp Scanner with appropriate insertion point types for the target application
- Use targeted scanning for specific data structures (JSON, XML, GraphQL)
- Set up crawl-and-scan workflows for comprehensive coverage
- Always verify scanner findings manually before reporting
- Use Burp's extension ecosystem for specialized testing

### Key Takeaways

- This lab demonstrates a essential skills vulnerability in a real-world scenario.
- The vulnerability occurs because user input reaches a sensitive operation without proper validation.
- The PortSwigger lab confirms: "This lab contains a vulnerability that enables you to read arbitrary files from the server. To solve"
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Configure Burp Scanner with appropriate insertion point types for the target application
