# Stealing OAuth access tokens via a proxy page

### Goal -

Solve the PortSwigger lab: Stealing OAuth access tokens via a proxy page

### Exploitation

1. Identify the vulnerability type and injection point
2. Craft the appropriate payload
3. Deliver the payload and verify the result

### Why It Works

The exploit succeeds because this lab uses an oauth service to allow users to log in with their social media account. flawed validation by the oauth service makes it possible for an attacker to leak access tokens to arbitrary pag

The official solution confirms: Study the OAuth flow while proxying traffic through Burp. Using the same method as in the previous lab, identify that the redirect_uri is vulnerable t

The root cause is a failure in the application's security architecture specific to this oauth scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab uses an OAuth service to allow users to log in with their social media account. Flawed vali"
- Validate redirect_uri with exact match against a server-side allowlist.

## PortSwigger Lab

**Official lab:** Stealing OAuth access tokens via a proxy page

**PortSwigger:** https://portswigger.net/web-security/oauth/lab-oauth-stealing-oauth-access-tokens-via-a-proxy-page
