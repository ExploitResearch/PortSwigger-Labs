# Accessing private GraphQL posts

### Goal -

Solve the PortSwigger lab: Accessing private GraphQL posts

### Exploitation

1. Identify the vulnerability type and injection point
2. Craft the appropriate payload
3. Deliver the payload and verify the result

### Why It Works

The exploit succeeds because the blog page for this lab contains a hidden blog post that has a secret password. to solve the lab, find the hidden blog post and enter the password.

The official solution confirms: Identify the vulnerability In Burp's browser, access the blog page.

The root cause is a failure in the application's security architecture specific to this graphql scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- This lab contains hidden blog post that has a secret password, demonstrating how graphql vulnerabilities manifest in real applications.
- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "The blog page for this lab contains a hidden blog post that has a secret password. To solve the lab,"
- Disable introspection in production and enforce per-field authorization.

## PortSwigger Lab

**Official lab:** Accessing private GraphQL posts

**PortSwigger:** https://portswigger.net/web-security/graphql/lab-graphql-reading-private-posts
