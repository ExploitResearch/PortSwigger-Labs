# Modifying serialized objects

### Goal -

Solve the PortSwigger lab: Modifying serialized objects


### Vulnerability / Concept

This lab demonstrates a vulnerability in the deserialization category.

This lab uses a serialization-based session mechanism and is vulnerable to privilege escalation as a result. To solve the lab, edit the serialized object in the session cookie to exploit this vulnerability and gain administrative privileges. Then, delete the user
            carlos.

The vulnerability exists because the application fails to properly validate, sanitize, or secure the user-controlled input that reaches a sensitive operation. The specific attack surface and exploitation technique depend on the exact vulnerability type demonstrated in this lab.

### Recon / Initial Analysis

Based on the lab's objective and the PortSwigger solution:

1. Analyze the application's functionality to identify the attack surface
2. Log in using your own credentials. Notice that the post-login GET /my-account request contains a session cookie that appears to be URL and Base64-encoded.
                    
                    
   
3. Use Burp Suite Proxy to intercept and analyze requests
4. Identify the specific vulnerability type by testing user-controlled input
5. Determine the appropriate exploitation technique for this lab

### Exploitation

1. Identify the serialization format (PHP, Java, Ruby, Python, .NET)
2. Decode and modify the serialized object to change properties
3. Re-encode and submit the modified serialized data
4. For RCE: research and use known gadget chains for the target framework

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab uses a serialization-based session mechanism and is vulnerable to privilege escalation as a result. To solve the lab, edit the serialized object in the session cookie to exploit this vulnerab"

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

An attacker could modify object properties to bypass authentication or escalate privileges, execute arbitrary code via gadget chains (RCE), access or modify sensitive data, or cause denial of service.

### Detection / Testing Methodology

1. Identify serialized data in cookies, parameters, or hidden fields
2. Decode the serialized data to identify the format
3. Look for object properties that control application behavior
4. Research known gadget chains for the target language/framework
5. Test modifying object properties (admin flag, user role)
6. For RCE: research and use known gadget chains
7. Check for PHAR deserialization in PHP applications

### Remediation

- Never deserialize untrusted data
- Use signed/encrypted serialization for sensitive data
- Implement allowlists for deserializable types
- Use JSON instead of native serialization
- Keep deserialization libraries updated
- Run deserialization in isolated environments
- Monitor for deserialization anomalies

### Key Takeaways

- This lab demonstrates a deserialization vulnerability in a real-world scenario.
- The vulnerability occurs because user input reaches a sensitive operation without proper validation.
- The PortSwigger lab confirms: "This lab uses a serialization-based session mechanism and is vulnerable to privilege escalation as a"
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Never deserialize untrusted data
