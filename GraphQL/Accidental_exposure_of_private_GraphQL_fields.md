# Accidental exposure of private GraphQL fields

### Goal -

Solve the PortSwigger lab: Accidental exposure of private GraphQL fields

### Exploitation

1. Identify the vulnerability type and injection point
2. Craft the appropriate payload
3. Deliver the payload and verify the result

### Why It Works

The exploit succeeds because the user management functions for this lab are powered by a graphql endpoint. the lab contains an access control vulnerability whereby you can induce the api to reveal user credential fields.

The official solution confirms: Identify the vulnerability In Burp's browser, access the lab and select My account.

The root cause is a failure in the application's security architecture specific to this graphql scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- This lab contains access control vulnerability whereby you can, demonstrating how graphql vulnerabilities manifest in real applications.
- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "The user management functions for this lab are powered by a GraphQL endpoint. The lab contains an ac"
- Disable introspection in production and enforce per-field authorization.
