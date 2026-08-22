# Bypassing AI scanner defenses to exfiltrate sensitive information

### Goal -

Solve the PortSwigger lab: Bypassing AI scanner defenses to exfiltrate sensitive information


### Vulnerability / Concept

This lab demonstrates a vulnerability in the llm attacks category.

This lab features an AI-powered scanner that has access to sensitive user data, including API keys, while performing site audits. The scanner has been given the login credentials for carlos so it can explore authenticated areas of the site.

The vulnerability exists because the application fails to properly validate, sanitize, or secure the user-controlled input that reaches a sensitive operation. The specific attack surface and exploitation technique depend on the exact vulnerability type demonstrated in this lab.

### Recon / Initial Analysis

Based on the lab's objective and the PortSwigger solution:

1. Analyze the application's functionality to identify the attack surface
2. The solution for this lab will be published shortly. Check back soon.
3. Use Burp Suite Proxy to intercept and analyze requests
4. Identify the specific vulnerability type by testing user-controlled input
5. Determine the appropriate exploitation technique for this lab

### Exploitation

1. Interact with the LLM to understand its capabilities and API access
2. Craft a prompt that exploits the specific vulnerability (excessive agency, indirect injection, or insecure output)
3. Use the LLM's API access to perform the attack (delete users, exfiltrate data, etc.)

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab features an AI-powered scanner that has access to sensitive user data, including API keys, while performing site audits. The scanner has been given the login credentials for carlos so it can "

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

An attacker could exploit LLM API access to delete accounts, modify data, perform unauthorized actions, inject instructions via data sources (indirect prompt injection), use LLM output to achieve XSS, exfiltrate sensitive data, or cause destructive actions via AI agents.

### Detection / Testing Methodology

1. Identify the LLM-powered feature (chatbot, assistant, content generator)
2. Map what APIs the LLM has access to by asking it directly
3. Test if the LLM processes untrusted input from data sources
4. Check if LLM output is rendered without sanitization
5. Test if the LLM can be tricked into making unauthorized API calls
6. Check for excessive agency (can the LLM delete/modify data?)
7. Test for indirect prompt injection via product descriptions, reviews, etc.

### Remediation

- Follow least-privilege principles for LLM API access
- Implement human-in-the-loop approval for destructive actions
- Isolate LLM processing of untrusted data (indirect prompt injection defense)
- Sanitize all LLM output before rendering (prevent XSS)
- Monitor and rate-limit LLM API calls
- Use separate LLM instances for trusted vs untrusted data
- Block destructive operations by default
- Log all LLM API calls for forensics

### Key Takeaways

- This lab demonstrates a llm attacks vulnerability in a real-world scenario.
- The vulnerability occurs because user input reaches a sensitive operation without proper validation.
- The PortSwigger lab confirms: "This lab features an AI-powered scanner that has access to sensitive user data, including API keys, "
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Follow least-privilege principles for LLM API access
