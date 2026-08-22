# SameSite Strict bypass via sibling domain

### Goal - 

Perform a cross-site websocket hijacking attack to exfiltrate the victim's chat history and compromise the victim's account.



### Vulnerability / Concept

This lab demonstrates a vulnerability in the csrf category.

This lab's live chat feature is vulnerable to cross-site WebSocket hijacking (CSWSH). To solve the lab, log in to the victim's account.

The vulnerability exists because the application fails to properly validate, sanitize, or secure the user-controlled input that reaches a sensitive operation. The specific attack surface and exploitation technique depend on the exact vulnerability type demonstrated in this lab.

### Recon / Initial Analysis

1. Analyze the application's functionality and identify user-controlled inputs
2. Use Burp Suite to intercept and modify requests
3. Test for the specific csrf vulnerability
4. Identify the injection point and context
5. Craft an appropriate payload

### Analysis/Exploitation -

It uses WebSocket in the chat:

```html
var webSocket = new WebSocket(chatForm.getAttribute("action"));
```

We also see that function `sendMessage()` is calling function `htmlEncode()` to HTML encode our input:

```html
function htmlEncode(str) {
    if (chatForm.getAttribute("encode")) {
        return String(str).replace(/['"<>&\r\n\\]/gi, function (c) {
            var lookup = {'\\': '&#x5c;', '\r': '&#x0d;', '\n': '&#x0a;', '"': '&quot;', '<': '&lt;', '>': '&gt;', "'": '&#39;', '&': '&amp;'};
            return lookup[c];
        });
    }
    return str;
}
```

it HTML encodes many characters. So normal DOM-based XSS won’t exploitable.

However, since it’s using WebSocket to communicate the chat, **we can try to test CSWSH (Cross-Site WebSocket Hijacking).**

First, let’s send a test message, and intercept all WebSocket requests via Burp Suite:

In the above WebSocket requests, we can see that **it’s vulnerable to CSRF(Cross-Site Request Forgery), as there is no CSRF token or unpredictable values in request parameters.**

**Then, we can refresh the page:**

It’ll send a `READY` message to render all chat messages.

If the WebSocket handshake request is vulnerable to CSRF, then an 
attacker’s web page can perform a cross-site request to open a WebSocket
 on the vulnerable site!

**To do so, I’ll craft a HTML form that automatically send a WebSocket request to **`/chat`** with message **`READY`**, and exfiltrate the victim’s chat history:**

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab's live chat feature is vulnerable to cross-site WebSocket hijacking (CSWSH). To solve the lab, log in to the victim's account."

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

An attacker could change the victim's email address (account takeover via password reset), transfer funds, modify account settings (disable 2FA), delete data, or perform any action the victim is authorized to perform.

### Detection / Testing Methodology

1. Identify state-changing endpoints (POST/PUT/DELETE)
2. Check if the application uses CSRF tokens
3. Examine how tokens are validated (presence, session-binding, method-dependence)
4. Test if SameSite cookie attributes are set
5. Check if Referer/Origin header validation is performed
6. Attempt to submit a cross-origin form without the token

### Remediation

- Use CSRF tokens that are unique per session and validated server-side
- Implement SameSite=Strict or SameSite=Lax on session cookies
- Validate the Referer or Origin header on state-changing requests
- Require re-authentication for critical actions
- Never perform state-changing operations via GET requests

### Key Takeaways

- This lab demonstrates a csrf vulnerability in a real-world scenario.
- The vulnerability occurs because user input reaches a sensitive operation without proper validation.
- The PortSwigger lab confirms: "This lab's live chat feature is vulnerable to cross-site WebSocket hijacking (CSWSH). To solve the l"
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Use CSRF tokens that are unique per session and validated server-side
