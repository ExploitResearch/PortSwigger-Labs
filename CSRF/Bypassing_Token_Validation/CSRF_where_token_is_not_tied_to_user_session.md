# CSRF where token is not tied to user session

### Goal - 

use your exploit server to host an HTML page that uses a CSRF attack to change the viewer’s email address.

Credentials - wiener:peter, carlos:montoya



### Vulnerability / Concept

This lab demonstrates a vulnerability in the csrf category.

This lab's email change functionality is vulnerable to CSRF. It uses tokens to try to prevent CSRF attacks, but they aren't integrated into the site's session handling system.

The vulnerability exists because the application fails to properly validate, sanitize, or secure the user-controlled input that reaches a sensitive operation. The specific attack surface and exploitation technique depend on the exact vulnerability type demonstrated in this lab.

### Recon / Initial Analysis

Based on the lab's objective and the PortSwigger solution:

1. Analyze the application's functionality to identify the attack surface
2. Open Burp's browser and log in to your account. Submit the "Update email" form, and intercept the resulting request.
                    
                    
                        Make a note of th
3. Use Burp Suite Proxy to intercept and analyze requests
4. Identify the specific vulnerability type by testing user-controlled input
5. Determine the appropriate exploitation technique for this lab

### Analysis/Exploitation -

Login as user `wiener`:

Inspect the form and notice that when we refresh the page (ie: on each request of the`/my-account`) each time csrf token gets change even within a session

![](./images/ef68f1710266_001.png)

**Check whether the tokens are bound to the sessions. **

I reload the `/my-account` page a few times, logout and login again (all as `wiener`).

Now I use Repeater to take one of my old email change requests, copy the new session data from the fresh login inside and a CSRF-token from before the logout:

![](./images/ef68f1710266_002.png)

And the email change goes through. This means that the tokens are not bound to the current session, which is a serious flaw.

**The next step is to find out whether the tokens are bound to the user.**

Login as user `carlos` in incognito:

Submit the "Update email" form, and intercept the resulting request.

**use user **`wiener`** CSRF token in user **`carlos`

![](./images/ef68f1710266_003.png)

The request is accepted and carlos email get changed

![](./images/ef68f1710266_004.png)

{% hint style="info" %}
💡 In order for a CSRF attack to be possible:

  - A relevant action: change a users email
  - Cookie-based session handling: session cookie
  - No unpredictable request parameters: csrf token is not tied to user session

Testing CSRF Tokens:

  1. Remove the CSRF token and see if application accepts request
  1. Change the request method from POST to GET
  1. See if csrf token is tied to user session
{% endhint %}


{% hint style="info" %}
💡 Note that the CSRF tokens are single-use, so you'll need to include a fresh one.
we also need to use new email and can’t use email assigned to other users.

The next steps are easy:

- Prepare the HTML form for the email change
- Use one of the existing but not used CSRF-tokens
- Add an auto-submit feature

In Burp Suite Professional, right-click on the request, and from the context menu select Engagement tools / Generate CSRF PoC. Enable the option to include an auto-submit script and click "Regenerate".

Go to the exploit server, paste your exploit HTML into the "Body" section, and click "Store".

We can test it locally via the `View exploit` button

- Change the email address in your exploit so that it doesn't match your own or in use of other user and use new csrf token
- Store the exploit, then click "Deliver to victim" to solve the lab.
{% endhint %}

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab's email change functionality is vulnerable to CSRF. It uses tokens to try to prevent CSRF attacks, but they aren't integrated into the site's session handling system."

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
- The PortSwigger lab confirms: "This lab's email change functionality is vulnerable to CSRF. It uses tokens to try to prevent CSRF a"
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Use CSRF tokens that are unique per session and validated server-side
