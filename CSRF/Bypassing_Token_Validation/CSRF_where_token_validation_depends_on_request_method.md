# CSRF where token validation depends on request method

### Goal - 

use your exploit server to host an HTML page that uses a CSRF attack to change the viewer’s email address.



### Vulnerability / Concept

This lab demonstrates a vulnerability in the csrf category.

This lab's email change functionality is vulnerable to CSRF.

The vulnerability exists because the application fails to properly validate, sanitize, or secure the user-controlled input that reaches a sensitive operation. The specific attack surface and exploitation technique depend on the exact vulnerability type demonstrated in this lab.

### Recon / Initial Analysis

Based on the lab's objective and the PortSwigger solution:

1. Analyze the application's functionality to identify the attack surface
2. Open Burp's browser and log in to your account. Submit the "Update email" form, and find the resulting request in your Proxy history.
                    
                    
                        
3. Use Burp Suite Proxy to intercept and analyze requests
4. Identify the specific vulnerability type by testing user-controlled input
5. Determine the appropriate exploitation technique for this lab

### Analysis/Exploitation -

Login as user `wiener`:

Update the email 

![](./images/5281dc080ffc_001.png)

When we click the `Update email` button, it’ll send a POST request to `/my-account/change-email` with the parameter `email & csrf  `

check what happens when I simply remove the CSRF-token from the request we get <span style="color: #E03E1B">Missing parameter 'csrf'</span>

![](./images/5281dc080ffc_002.png)

The same happens if I try to use an empty token (`&csrf=`) or random token  (`&csrf=1234asdf`) 

we can’t modify our email address, as the form is missing the right CSRF token!

To bypass the CSRF token, we can try to change our method from POST to GET by selecting `Change request method` from the context menu.

![](./images/5281dc080ffc_003.png)

Here we don’t get any error and We’ve successfully changed the email address to attacker’s controlled value

{% hint style="info" %}
💡 In order for a CSRF attack to be possible:

  - A relevant action: change a users email
  - Cookie-based session handling: session cookie
  - No unpredictable request parameters: Request method can be changed to GET which does not require CSRF token
{% endhint %}


If you're using Burp Suite Professional, right-click on the request, and from the context menu select Engagement tools / Generate CSRF PoC. Enable the option to include an auto-submit script and click "Regenerate". 

In the community edition, simply get the the form from the HTML of the application and perform the required changes to it (specifically: change the method and action, remove the csrf token and add the auto-submit script)

![](./images/5281dc080ffc_004.png)

- Go to the exploit server, paste your exploit HTML into the "Body" section, and click "Store".
- To verify if the exploit will work, try it on yourself by clicking "View exploit" and checking the resulting HTTP request and response.
- Change the email address in your exploit so that it doesn't match your own.
- Store the exploit, then click "Deliver to victim" to solve the lab.

![](./images/5281dc080ffc_005.png)

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab's email change functionality is vulnerable to CSRF."

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
- The PortSwigger lab confirms: "This lab's email change functionality is vulnerable to CSRF."
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Use CSRF tokens that are unique per session and validated server-side
