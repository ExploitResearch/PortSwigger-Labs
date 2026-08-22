# 0.CL request smuggling

### Goal -

Solve the PortSwigger lab: 0.CL request smuggling

### Exploitation

1. Identify the smuggling variant (CL.TE, TE.CL, TE.TE, H2.CL, etc.)
2. Craft a smuggled request that will be processed by the back-end server
3. The smuggled request can bypass front-end security controls, capture other users' requests, or poison the cache

### Why It Works

The exploit succeeds because carlos visits the homepage every five seconds. to solve the lab, exploit the vulnerability to execute alert() in his browser.

The root cause is a failure in the application's security architecture specific to this request smuggling scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "Carlos visits the homepage every five seconds. To solve the lab, exploit the vulnerability to execut"
- Reject requests with both Content-Length and Transfer-Encoding headers.
