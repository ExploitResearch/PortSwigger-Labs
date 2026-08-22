# Server-side pause-based request smuggling

### Goal -

Solve the PortSwigger lab: Server-side pause-based request smuggling

### Exploitation

1. Identify the smuggling variant (CL.TE, TE.CL, TE.TE, H2.CL, etc.)
2. Craft a smuggled request that will be processed by the back-end server
3. The smuggled request can bypass front-end security controls, capture other users' requests, or poison the cache

### Why It Works

The exploit succeeds because this lab is vulnerable to pause-based server-side request smuggling. the front-end server streams requests to the back-end, and the back-end server does not close the connection after a timeout on som

The official solution confirms: Identify a desync vector In Burp, notice from the Server response header that the lab is using Apache 2.4.52. This version of Apache is potentially vu

The root cause is a failure in the application's security architecture specific to this request smuggling scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab is vulnerable to pause-based server-side request smuggling. The front-end server streams re"
- Reject requests with both Content-Length and Transfer-Encoding headers.
