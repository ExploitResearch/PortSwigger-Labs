# Cross-site WebSocket hijacking

### Goal -

Solve the PortSwigger lab: Cross-site WebSocket hijacking


### Vulnerability / Concept

This lab demonstrates a vulnerability in the websockets category.

To solve the lab, use the exploit server to host an HTML/JavaScript payload that uses a cross-site WebSocket hijacking attack to exfiltrate the victim's chat history, then use this gain access to their account.

The vulnerability exists because the application fails to properly validate, sanitize, or secure the user-controlled input that reaches a sensitive operation. The specific attack surface and exploitation technique depend on the exact vulnerability type demonstrated in this lab.

### Recon / Initial Analysis

Based on the lab's objective and the PortSwigger solution:

1. Analyze the application's functionality to identify the attack surface
2. Click "Live chat" and send a chat message.
                    
                    
                        Reload the page.
                    
                    
                        In Burp 
3. Use Burp Suite Proxy to intercept and analyze requests
4. Identify the specific vulnerability type by testing user-controlled input
5. Determine the appropriate exploitation technique for this lab

### Exploitation

1. For message injection: craft malicious WebSocket messages with payloads
2. For cross-site hijacking: create a malicious page that opens a WebSocket to the target
3. For handshake manipulation: modify headers in the initial HTTP upgrade request

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "To solve the lab, use the exploit server to host an HTML/JavaScript payload that uses a cross-site WebSocket hijacking attack to exfiltrate the victim's chat history, then use this gain access to thei"

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

An attacker could inject malicious WebSocket messages to perform actions as the victim, hijack WebSocket connections across origins, bypass authentication on the WebSocket handshake, or exfiltrate real-time data.

### Detection / Testing Methodology

1. Identify WebSocket connections in Burp Proxy (filter by WebSocket protocol)
2. Inspect WebSocket messages for user-controlled input
3. Check if the WebSocket handshake uses CSRF tokens or origin validation
4. Test if the handshake accepts cross-origin connections
5. Test for message injection and manipulation
6. Check for cross-site WebSocket hijacking

### Remediation

- Validate and sanitize all WebSocket messages like any HTTP input
- Implement origin checking on WebSocket handshakes
- Use CSRF tokens for WebSocket upgrade requests
- Implement authentication on the WebSocket handshake
- Monitor for unusual WebSocket message patterns
- Use wss:// (WebSocket Secure) to prevent eavesdropping

### Key Takeaways

- This lab demonstrates a websockets vulnerability in a real-world scenario.
- The vulnerability occurs because user input reaches a sensitive operation without proper validation.
- The PortSwigger lab confirms: "To solve the lab, use the exploit server to host an HTML/JavaScript payload that uses a cross-site W"
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Validate and sanitize all WebSocket messages like any HTTP input
