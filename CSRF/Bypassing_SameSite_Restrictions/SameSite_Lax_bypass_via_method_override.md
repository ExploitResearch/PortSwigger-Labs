# SameSite Lax bypass via method override

### Goal -

Bypass SameSite=Lax cookie restrictions by using a method override technique.


### Vulnerability / Concept

Cross-Site Request Forgery (CSRF) is a web security vulnerability that allows an attacker to induce users to perform actions that they did not intend to perform. It occurs when an application relies solely on cookies for session management without validating that the request originated from the legitimate user's own actions.

CSRF attacks exploit the browser's automatic inclusion of cookies in cross-origin requests. If the victim is authenticated to the target application, the attacker's forged request carries the victim's session cookie, making it appear legitimate to the server.

Key conditions for CSRF: (1) A relevant state-changing action exists, (2) Session management is cookie-based, (3) No unpredictable request parameters (like CSRF tokens) are required.

### Recon / Initial Analysis

1. Identify state-changing endpoints (POST/PUT/DELETE requests that modify data)
2. Check if the application uses CSRF tokens in forms or headers
3. Examine how tokens are validated (presence, session-binding, method-dependence)
4. Test if SameSite cookie attributes are set on session cookies
5. Check if Referer header validation is performed
6. Verify if token validation can be bypassed by removing the token or changing the request method

### Vulnerability / Concept

SameSite=Lax cookies are sent with GET requests but not POST. If the application supports method override (e.g., `_method=POST` parameter), the attacker can perform a CSRF via a GET request that the server treats as a POST.

### Exploitation

1. Identify that the target cookie has SameSite=Lax
2. Check if the application supports method override parameters (e.g., `_method`, `X-HTTP-Method-Override`)
3. Craft a GET request with the method override parameter set to POST
4. The server processes it as a POST while the browser sends it as a GET (bypassing SameSite=Lax)

### Why It Works

The vulnerability exists because the server trusts that any request bearing the victim's session cookie was intentionally initiated by the victim. Without anti-CSRF tokens, SameSite cookie restrictions, or Referer validation, the server cannot distinguish between a legitimate request from the user and a forged request from an attacker's page.

The broken trust boundary is between the browser and the server: the browser automatically attaches cookies to any request to the target domain, regardless of which site initiated the request. This design feature of HTTP cookies becomes a security flaw when the server treats cookie presence as proof of user intent.

### Real-World Impact

An attacker could trick an authenticated user into:
- Changing their email address (account takeover via password reset)
- Transferring funds to the attacker's account
- Modifying account settings (disabling 2FA, changing security questions)
- Deleting or modifying critical data
- Elevating privileges if the victim has admin access
- Performing any action the victim is authorized to perform

### Remediation

- Use CSRF tokens that are unique per session and validated server-side on every state-changing request
- Implement SameSite=Strict or SameSite=Lax on session cookies
- Validate the Referer or Origin header on state-changing requests
- Require re-authentication for critical actions (password change, email change, fund transfers)
- Use the Double Submit Cookie pattern as additional defense-in-depth

### Key Takeaways

- CSRF exploits the browser's automatic cookie inclusion — the server cannot verify request origin without additional checks.
- CSRF tokens must be unique per session and validated server-side — their mere presence is not enough.
- SameSite cookie restrictions provide a strong first line of defense but are not a complete solution.
- Referer/Origin validation adds another layer but can be bypassed if not implemented correctly.
- State-changing operations must never be performed via GET requests.
