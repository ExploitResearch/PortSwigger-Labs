# Detecting NoSQL injection

### Goal -

Solve the PortSwigger lab: Detecting NoSQL injection

### Exploitation

1. Identify the injection point in the application
2. Craft a NoSQL injection payload appropriate for the target database
3. Test the payload and analyze the response


### Why It Works

The exploit succeeds because the product category filter for this lab is powered by a mongodb nosql database. it is vulnerable to nosql injection.

The official solution confirms: In Burp's browser, access the lab and click on a product category filter. In Burp, go to Proxy &gt; HTTP history. Right-click the category f

The root cause is a failure in the application's security architecture specific to this nosql injection scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- The PortSwigger lab description confirms: "The product category filter for this lab is powered by a MongoDB NoSQL database. It is vulnerable to"
- Parameterized queries would prevent this vulnerability entirely.
