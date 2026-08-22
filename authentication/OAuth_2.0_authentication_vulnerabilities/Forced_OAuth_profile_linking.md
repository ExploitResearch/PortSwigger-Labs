# Forced OAuth profile linking

### Goal -

Solve the PortSwigger lab: Forced OAuth profile linking

### Exploitation

1. Identify the vulnerability type and injection point
2. Craft the appropriate payload
3. Deliver the payload and verify the result

### Why It Works

The exploit succeeds because this lab gives you the option to attach a social media profile to your account so that you can log in via oauth instead of using the normal username and password. due to the insecure implementation of

The official solution confirms: While proxying traffic through Burp, click "My account". You are taken to a normal login page, but notice that there is an option to log in using your

The root cause is a failure in the application's security architecture specific to this oauth scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab gives you the option to attach a social media profile to your account so that you can log i"
- Validate redirect_uri with exact match against a server-side allowlist.

## PortSwigger Lab

**Official lab:** Forced OAuth profile linking

**PortSwigger:** https://portswigger.net/web-security/oauth/lab-oauth-forced-oauth-profile-linking
