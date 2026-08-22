# Finding a hidden GraphQL endpoint

### Goal -

Solve the PortSwigger lab: Finding a hidden GraphQL endpoint

### Exploitation

1. Identify the vulnerability type and injection point
2. Craft the appropriate payload
3. Deliver the payload and verify the result

### Why It Works

The exploit succeeds because the user management functions for this lab are powered by a hidden graphql endpoint. you won't be able to find this endpoint by simply clicking pages in the site. the endpoint also has some defenses a

The official solution confirms: Find the hidden GraphQL endpoint In Repeater, send requests to some common GraphQL endpoint suffixes and inspect the results.

The root cause is a failure in the application's security architecture specific to this graphql scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "The user management functions for this lab are powered by a hidden GraphQL endpoint. You won't be ab"
- Disable introspection in production and enforce per-field authorization.

## PortSwigger Lab

**Official lab:** Finding a hidden GraphQL endpoint

**PortSwigger:** https://portswigger.net/web-security/graphql/lab-graphql-find-the-endpoint
