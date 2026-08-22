# SSRF via OpenID dynamic client registration

### Goal -

Solve the PortSwigger lab: SSRF via OpenID dynamic client registration

### Exploitation

1. Identify the vulnerability type and injection point
2. Craft the appropriate payload
3. Deliver the payload and verify the result

### Why It Works

The exploit succeeds because this lab allows client applications to dynamically register themselves with the oauth service via a dedicated registration endpoint. some client-specific data is used in an unsafe way by the oauth ser

The official solution confirms: While proxying traffic through Burp, log in to your own account. Browse to https://oauth-YOUR-OAUTH-SERVER.oauth-server.net/.well-known/openid-configu

The root cause is a failure in the application's security architecture specific to this oauth scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab allows client applications to dynamically register themselves with the OAuth service via a "
- Validate redirect_uri with exact match against a server-side allowlist.

## PortSwigger Lab

**Official lab:** SSRF via OpenID dynamic client registration

**PortSwigger:** https://portswigger.net/web-security/oauth/openid/lab-oauth-ssrf-via-openid-dynamic-client-registration
