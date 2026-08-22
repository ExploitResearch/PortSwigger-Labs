# Accidental exposure of private GraphQL fields

**Lab URL:** https://portswigger.net/web-security/graphql/lab-graphql-accidental-field-exposure

### Goal -

Solve the PortSwigger lab: Accidental exposure of private GraphQL fields

### Exploitation

1. Identify the vulnerability type and injection point
2. Craft the appropriate payload
3. Deliver the payload and verify the result

### Why It Works

The application has a access control vulnerability in the application, which can be exploited by crafting input that bypasses the insufficient validation in place.

### Key Takeaways

- The access control vulnerability is exploitable because user input is processed without adequate validation.
