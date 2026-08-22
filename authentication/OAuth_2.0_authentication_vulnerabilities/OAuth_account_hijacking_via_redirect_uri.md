# OAuth account hijacking via redirect_uri

### Goal -

Solve the PortSwigger lab: OAuth account hijacking via redirect_uri

### Exploitation

1. Identify the vulnerability type and injection point
2. Craft the appropriate payload
3. Deliver the payload and verify the result

### Why It Works

The exploit succeeds because this lab uses an oauth service to allow users to log in with their social media account. a misconfiguration by the oauth provider makes it possible for an attacker to steal authorization codes associa

The official solution confirms: While proxying traffic through Burp, click "My account" and complete the OAuth login process. Afterwards, you will be redirected back to the blog webs

The root cause is a failure in the application's security architecture specific to this oauth scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab uses an OAuth service to allow users to log in with their social media account. A misconfig"
- Validate redirect_uri with exact match against a server-side allowlist.

## PortSwigger Lab

**Official lab:** OAuth account hijacking via redirect_uri

**PortSwigger:** https://portswigger.net/web-security/oauth/lab-oauth-account-hijacking-via-redirect-uri
