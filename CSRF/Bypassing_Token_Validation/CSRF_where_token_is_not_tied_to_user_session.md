# CSRF where token is not tied to user session

### Goal - 

use your exploit server to host an HTML page that uses a CSRF attack to change the viewer’s email address.

Credentials - wiener:peter, carlos:montoya

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

The exploit succeeds because this lab's email change functionality is vulnerable to csrf. it uses tokens to try to prevent csrf attacks, but they aren't integrated into the site's session handling system.

The official solution confirms: Open Burp's browser and log in to your account. Submit the "Update email" form, and intercept the resulting request. Make a note of the value of the C

The root cause is a failure in the application's security architecture specific to this csrf scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab's email change functionality is vulnerable to CSRF. It uses tokens to try to prevent CSRF a"
- CSRF tokens, SameSite cookies, and Referer validation together provide defense-in-depth.

## PortSwigger Lab

**Official lab:** CSRF where token is not tied to user session

**PortSwigger:** https://portswigger.net/web-security/csrf/bypassing-token-validation/lab-token-not-tied-to-user-session
