# Clickjacking with a frame buster script

### Goal -

Bypass a frame-busting JavaScript to perform a clickjacking attack.



### Vulnerability / Concept

This lab demonstrates a vulnerability in the clickjacking category.

This lab is protected by a frame buster which prevents the website from being framed. Can you get around the frame buster and conduct a clickjacking attack that changes the users email address?

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

1. Verify the page has a frame-busting script (check source code)
2. Create an iframe with `sandbox='allow-scripts allow-forms'` (without `allow-top-navigation`)
3. The sandbox prevents the frame-buster from redirecting the top window
4. Overlay deceptive UI elements on the framed page

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab is protected by a frame buster which prevents the website from being framed. Can you get around the frame buster and conduct a clickjacking attack that changes the users email address?"

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
- The PortSwigger lab confirms: "This lab is protected by a frame buster which prevents the website from being framed. Can you get ar"
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Set X-Frame-Options: DENY or SAMEORIGIN
