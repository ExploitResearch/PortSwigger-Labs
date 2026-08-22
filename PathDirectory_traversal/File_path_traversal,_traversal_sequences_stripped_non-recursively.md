# File path traversal, traversal sequences stripped non-recursively

### Goal - 

Retrieve the contents of the `/etc/passwd` file.


### Vulnerability / Concept

This lab demonstrates a web security vulnerability that can be exploited to compromise the application's security. The vulnerability allows an attacker to bypass security controls and perform unauthorized actions.

The core issue is a failure in the application's security architecture — either insufficient input validation, broken access controls, improper trust boundaries, or insecure handling of user-supplied data. Understanding the root cause is essential for both exploitation and remediation.

### Recon / Initial Analysis

1. Identify the attack surface — what user-controlled inputs exist (URL parameters, form fields, headers, cookies)
2. Analyze the application's behavior with unexpected input
3. Map the request flow and identify trust boundaries
4. Test for error messages that reveal implementation details
5. Compare authenticated vs unauthenticated behavior
6. Use Burp Suite Proxy to capture and analyze all requests
7. Check for hidden parameters using Burp Intruder or Param Miner

### Analysis/Exploitation 

open any product or open any image in new tab

![](./images/58831d32ca9e_001.png)

apply above filter to see image request and sent it to repeater

![](./images/58831d32ca9e_002.png)

As written in the lab description, using simple path traversal sequences like `../` does not lead to an actual path traversal. If the sequences are stripped from the user input in a naive way, it just removes all occurrences of `../` from the filename.

An input of `../../../etc/passwd` will therefore become the relative path `etc/passwd` which does not exist. Using `..//etc/passwd` in an attempt to create an absolute `/etc/passwd` does not find any file either.

But if just literal `../` sequences are removed, we simply need to provide a string that represents a path traversal string after the removal. Therefore `....//` will become `../` (the first two dots and the second slash remain after `../` is removed). `..././` works as well.

{% hint style="info" %}
💡 To obtain a result of `../../../etc/passwd`, I request the image file  `....//....//....//etc/passwd`:
The application strips path traversal sequences from the user-supplied filename before using it. **To bypass that, we use nested traversal sequences, like **`....//`**:**
{% endhint %}


![](./images/58831d32ca9e_003.png)

### Why It Works

The vulnerability exists because the application fails to properly validate, sanitize, or authorize user input. The broken trust boundary allows an attacker to manipulate the application's behavior by injecting unexpected data that the server processes without adequate security checks.

### Real-World Impact

An attacker could exploit this vulnerability to:
- Access sensitive data belonging to other users
- Bypass authentication or authorization controls
- Perform unauthorized actions on behalf of legitimate users
- Potentially achieve remote code execution on the server
- Compromise the integrity or availability of the application

### Remediation

- Implement proper server-side input validation for all user-controlled data
- Use parameterized queries and prepared statements
- Enforce server-side authorization checks on every request
- Follow the principle of least privilege
- Implement security headers (CSP, X-Frame-Options, X-Content-Type-Options)
- Use a Web Application Firewall (WAF) as defense-in-depth
- Regularly test for vulnerabilities using automated scanners and manual testing

### Key Takeaways

- Never trust user-controlled input — validate and sanitize everything server-side.
- Security controls must be enforced server-side, not client-side.
- Understanding the vulnerability's root cause is essential for proper remediation.
- Burp Suite is essential for identifying and exploiting web vulnerabilities.
- Defense in depth — use multiple layers of protection, not just one.
