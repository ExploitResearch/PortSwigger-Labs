# Stored DOM XSS

## Metadata

| Property | Value |
|----------|-------|

---

### Target Goal 



### Vulnerability / Concept

This lab demonstrates a vulnerability in the cross site scripting category.

This lab demonstrates a stored DOM vulnerability in the blog comment functionality. To solve this lab, exploit this vulnerability to call the alert() function.

The vulnerability exists because the application fails to properly validate, sanitize, or secure the user-controlled input that reaches a sensitive operation. The specific attack surface and exploitation technique depend on the exact vulnerability type demonstrated in this lab.

### Recon / Initial Analysis

Based on the lab's objective and the PortSwigger solution:

1. Analyze the application's functionality to identify the attack surface
2. Post a comment containing the following vector:
				
                &lt;&gt;&lt;img src=1 onerror=alert(1)&gt;
				
					In an attempt to prevent XSS, the website uses the JavaScript replace() functi
3. Use Burp Suite Proxy to intercept and analyze requests
4. Identify the specific vulnerability type by testing user-controlled input
5. Determine the appropriate exploitation technique for this lab

### Analysis/Exploitation:

### analysing code

**In line 5, the **`comments`** variable is parsing an JSON object:**

```javascript
let comments = JSON.parse(this.responseText);
```

**Then in line 12-14, we can see that it’s escaping HTML code:**

```javascript
function escapeHTML(html) {
    return html.replace('<', '&lt;').replace('>', '&gt;');
}
```

**The **`<`** and **`>`** will be replaced as **`&lt;`** and **`&gt;`**.**

We also see that the JavaScript file uses `innerHTML` in `comment.author`, `comment.body`, which is a sink (Dangerous function).

`let newInnerHtml = firstPElement.innerHTML + escapeHTML(comment.author)`

Armed with above information, we can start to bypass the `<>` HTML encoding.

According to W3School, **the **`replace()`** method only replace the first instance.**

![](./images/56f22be1a806_001.png)

Which means if we add more than 1 `<` or `>`, it’ll be ignored.

**Let’s craft the XSS payload:**

```javascript
<><img src=errorpls onerror=alert(document.domain)>

```

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab demonstrates a stored DOM vulnerability in the blog comment functionality. To solve this lab, exploit this vulnerability to call the alert() function."

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
- The PortSwigger lab confirms: "This lab demonstrates a stored DOM vulnerability in the blog comment functionality. To solve this la"
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Use context-aware output encoding (HTML body, attribute, JavaScript string, URL)
