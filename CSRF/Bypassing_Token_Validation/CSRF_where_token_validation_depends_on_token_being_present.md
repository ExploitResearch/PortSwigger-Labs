# CSRF where token validation depends on token being present

### Goal - 

use your exploit server to host an HTML page that uses a CSRF attack to change the viewer’s email address.


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

### Analysis/Exploitation -

Login as user `wiener`:

Update the email 

![](./images/47db7cdfbca4_001.png)

 if I try to use an empty token (`&csrf=`) or random token  (`&csrf=1234asdf`) 

![](./images/47db7cdfbca4_002.png)

![](./images/47db7cdfbca4_003.png)

Delete the `csrf` parameter entirely and observe that the request is now accepted. So it only validate CSRF token if it is present in request

![](./images/47db7cdfbca4_004.png)

{% hint style="info" %}
💡 In order for a CSRF attack to be possible:

  - A relevant action: change a users email
  - Cookie-based session handling: session cookie
  - No unpredictable request parameters: csrf token is not mandatory

Testing CSRF Tokens:

  1. Change the request method from POST to GET
  1. Remove the CSRF token and see if application accepts request
{% endhint %}


In Burp Suite Professional, right-click on the request, and from the context menu select Engagement tools / Generate CSRF PoC. Enable the option to include an auto-submit script and click "Regenerate".

![](./images/47db7cdfbca4_005.png)

Go to the exploit server, paste your exploit HTML into the "Body" section, and click "Store".

We can test it locally via the `View exploit` button

- Change the email address in your exploit so that it doesn't match your own.
- Store the exploit, then click "Deliver to victim" to solve the lab.

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
