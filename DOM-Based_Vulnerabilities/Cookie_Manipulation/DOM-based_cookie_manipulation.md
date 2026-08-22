# DOM-based cookie manipulation

### Goal -

Solve the PortSwigger lab: DOM-based cookie manipulation

### Exploitation

1. Identify the vulnerability type and injection point
2. Craft the appropriate payload
3. Deliver the payload and verify the result

### Why It Works

The exploit succeeds because this lab demonstrates dom-based client-side cookie manipulation. to solve this lab, inject a cookie that will cause xss on a different page and call the print() function. you will need to use the expl

The official solution confirms: Notice that the home page uses a client-side cookie called lastViewedProduct, whose value is the URL of the last product page that the user visited. G

The root cause is a failure in the application's security architecture specific to this dom based scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab demonstrates DOM-based client-side cookie manipulation. To solve this lab, inject a cookie "
- Server-side validation and authorization are the primary defenses.
