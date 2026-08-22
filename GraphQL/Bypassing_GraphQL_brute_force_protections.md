# Bypassing GraphQL brute force protections

### Goal -

Solve the PortSwigger lab: Bypassing GraphQL brute force protections

### Exploitation

1. Identify the vulnerability type and injection point
2. Craft the appropriate payload
3. Deliver the payload and verify the result

### Why It Works

The exploit succeeds because the user login mechanism for this lab is powered by a graphql api. the api endpoint has a rate limiter that returns an error if it receives too many requests from the same origin in a short space of t

The official solution confirms: In Burp's browser, access the lab and select My account. Attempt to log in to the site using incorrect credentials.

The root cause is a failure in the application's security architecture specific to this graphql scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "The user login mechanism for this lab is powered by a GraphQL API. The API endpoint has a rate limit"
- Disable introspection in production and enforce per-field authorization.

## PortSwigger Lab

**Official lab:** Bypassing GraphQL brute force protections

**PortSwigger:** https://portswigger.net/web-security/graphql/lab-graphql-brute-force-protection-bypass
