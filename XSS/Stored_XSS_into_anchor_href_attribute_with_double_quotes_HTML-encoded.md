# Stored XSS into anchor href attribute with double quotes HTML-encoded

## Metadata

| Property | Value |
|----------|-------|

---

### Target Goal - 

Exploit stored XSS vulnerability to call the alert function



### Vulnerability / Concept

This lab demonstrates a vulnerability in the cross site scripting category.

This lab contains a stored cross-site scripting vulnerability in the comment functionality. To solve this lab, submit a comment that calls the alert function when the comment author name is clicked.

The vulnerability exists because the application fails to properly validate, sanitize, or secure the user-controlled input that reaches a sensitive operation. The specific attack surface and exploitation technique depend on the exact vulnerability type demonstrated in this lab.

### Recon / Initial Analysis

Based on the lab's objective and the PortSwigger solution:

1. Analyze the application's functionality to identify the attack surface
2. Post a comment with a random alphanumeric string in the "Website" input, then use Burp Suite to intercept the request and send it to Burp Repeater.
                    
                    
          
3. Use Burp Suite Proxy to intercept and analyze requests
4. Identify the specific vulnerability type by testing user-controlled input
5. Determine the appropriate exploitation technique for this lab

### Analysyis/Exploitation

![](./images/99de67491d5b_001.png)

![](./images/99de67491d5b_002.png)

after posting comment we can see that the url which we put in  website section is appearing in href 

instead of url we can insert script here

I tried to insert 

```javascript
<script>alert(1)</script>
"<script>alert(1)</script>
```

and when i clicked on comment they just get append at the end of our lab url and script didn’t work

![](./images/99de67491d5b_003.png)

### How to call javascript from a href

```javascript
<a href="#" onclick="myFunction()" >LinkText</a>
or
<a href="javascript:call_func();">...</a>
```

We can't use first one because double quotes are encode so we use 2nd method

```javascript
javascript:alert(1)
```

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab contains a stored cross-site scripting vulnerability in the comment functionality. To solve this lab, submit a comment that calls the alert function when the comment author name is clicked."

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

An attacker could steal session cookies, capture keystrokes (passwords, credit cards), perform actions on behalf of the victim, redirect users to phishing pages, deliver malware, or bypass CSRF protections.

### Detection / Testing Methodology

1. Identify input points reflected in the HTML response
2. Submit a unique marker (e.g., xssmarker123) to find exact reflection points
3. Determine the context: HTML body, attribute, JavaScript string, URL
4. Test which characters are encoded (<, >, ", ', `)
5. Test an appropriate proof-of-concept payload for the context
6. Confirm JavaScript execution
7. For DOM-based XSS: inspect JavaScript for dangerous sinks

### Remediation

- Use context-aware output encoding (HTML body, attribute, JavaScript string, URL)
- Use templating engines that auto-escape output
- Implement Content Security Policy (CSP) with script-src 'self' and nonces
- Set HttpOnly and Secure flags on session cookies
- Sanitize HTML input with allowlist-based libraries (DOMPurify)
- For DOM-based XSS: use textContent instead of innerHTML, avoid eval()

### Key Takeaways

- This lab demonstrates a cross site scripting vulnerability in a real-world scenario.
- The vulnerability occurs because user input reaches a sensitive operation without proper validation.
- The PortSwigger lab confirms: "This lab contains a stored cross-site scripting vulnerability in the comment functionality. To solve"
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Use context-aware output encoding (HTML body, attribute, JavaScript string, URL)
