# SSRF via OpenID dynamic client registration

### Goal -

Solve the PortSwigger lab: SSRF via OpenID dynamic client registration



### Vulnerability / Concept

This lab demonstrates a vulnerability in the oauth category.

This lab allows client applications to dynamically register themselves with the OAuth service via a dedicated registration endpoint. Some client-specific data is used in an unsafe way by the OAuth service, which exposes a potential vector for SSRF.

The vulnerability exists because the application fails to properly validate, sanitize, or secure the user-controlled input that reaches a sensitive operation. The specific attack surface and exploitation technique depend on the exact vulnerability type demonstrated in this lab.

### Recon / Initial Analysis

Based on the lab's objective and the PortSwigger solution:

1. Analyze the application's functionality to identify the attack surface
2. While proxying traffic through Burp, log in to your own account. Browse to https://oauth-YOUR-OAUTH-SERVER.oauth-server.net/.well-known/openid-configuration to access the configuration file. Notice th
3. Use Burp Suite Proxy to intercept and analyze requests
4. Identify the specific vulnerability type by testing user-controlled input
5. Determine the appropriate exploitation technique for this lab

### Exploitation

1. Identify the vulnerability type and injection point
2. Craft the appropriate payload
3. Deliver the payload and verify the result

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab allows client applications to dynamically register themselves with the OAuth service via a dedicated registration endpoint. Some client-specific data is used in an unsafe way by the OAuth ser"

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

An attacker could steal OAuth access tokens, hijack user accounts via redirect_uri manipulation, force-link their OAuth account to a victim's account, perform SSRF via OpenID dynamic client registration, or bypass authentication via OAuth implicit flow.

### Detection / Testing Methodology

1. Map the OAuth flow (authorization code, implicit, client credentials)
2. Test redirect_uri validation (exact match, prefix, wildcard)
3. Check if the state parameter is used and validated
4. Test for forced profile linking
5. Check if access tokens are exposed in URLs or logs
6. Test for SSRF via OpenID dynamic client registration
7. Check if PKCE is used

### Remediation

- Validate redirect_uri against a strict allowlist (exact match, not prefix/substring)
- Use the state parameter for CSRF protection
- Do not automatically link accounts without user confirmation
- Use PKCE (Proof Key for Code Exchange) for public clients
- Validate access tokens server-side before processing
- Do not pass access tokens in URLs (use Authorization header)

### Key Takeaways

- This lab demonstrates a oauth vulnerability in a real-world scenario.
- The vulnerability occurs because user input reaches a sensitive operation without proper validation.
- The PortSwigger lab confirms: "This lab allows client applications to dynamically register themselves with the OAuth service via a "
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Validate redirect_uri against a strict allowlist (exact match, not prefix/substring)
