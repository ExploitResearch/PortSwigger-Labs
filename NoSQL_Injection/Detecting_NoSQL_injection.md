# Detecting NoSQL injection

### Goal -

Solve the PortSwigger lab: Detecting NoSQL injection


### Vulnerability / Concept

This lab demonstrates a vulnerability in the nosql injection category.

The product category filter for this lab is powered by a MongoDB NoSQL database. It is vulnerable to NoSQL injection.

The vulnerability exists because the application fails to properly validate, sanitize, or secure the user-controlled input that reaches a sensitive operation. The specific attack surface and exploitation technique depend on the exact vulnerability type demonstrated in this lab.

### Recon / Initial Analysis

Based on the lab's objective and the PortSwigger solution:

1. Analyze the application's functionality to identify the attack surface
2. In Burp's browser, access the lab and click on a product category filter.
                                
                            
                            
                                
  
3. Use Burp Suite Proxy to intercept and analyze requests
4. Identify the specific vulnerability type by testing user-controlled input
5. Determine the appropriate exploitation technique for this lab

### Exploitation

1. Identify the injection point in the application
2. Craft a NoSQL injection payload appropriate for the target database
3. Test the payload and analyze the response

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "The product category filter for this lab is powered by a MongoDB NoSQL database. It is vulnerable to NoSQL injection."

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

An attacker could bypass authentication by injecting MongoDB operators ($ne, $gt, $regex), extract all database contents, modify or delete records, cause denial of service via expensive regex queries, or execute JavaScript if $where is allowed.

### Detection / Testing Methodology

1. Identify input fields that interact with NoSQL databases (login, search, API)
2. Test with NoSQL operators ($ne, $gt, $regex, $where)
3. Check if JSON objects are accepted as input (content type manipulation)
4. Test for boolean-based blind injection (compare responses)
5. Check for data extraction via $regex or $where
6. Look for operator injection in query parameters

### Remediation

- Validate input type (ensure strings are strings, not objects) before passing to database queries
- Use parameterized queries or ORM methods that prevent operator injection
- Implement input allowlists that reject $-prefixed keys in JSON input
- Disable JavaScript execution in NoSQL queries ($where)
- Apply least-privilege database accounts
- Use a WAF that understands NoSQL injection patterns

### Key Takeaways

- This lab demonstrates a nosql injection vulnerability in a real-world scenario.
- The vulnerability occurs because user input reaches a sensitive operation without proper validation.
- The PortSwigger lab confirms: "The product category filter for this lab is powered by a MongoDB NoSQL database. It is vulnerable to"
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Validate input type (ensure strings are strings, not objects) before passing to database queries
