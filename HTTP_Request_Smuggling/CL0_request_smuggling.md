# CL.0 request smuggling

### Goal -

Solve the PortSwigger lab: CL.0 request smuggling

### Exploitation

1. Identify the smuggling variant (CL.TE, TE.CL, TE.TE, H2.CL, etc.)
2. Craft a smuggled request that will be processed by the back-end server
3. The smuggled request can bypass front-end security controls, capture other users' requests, or poison the cache

### Why It Works

The exploit succeeds because this lab is vulnerable to cl.0 request smuggling attacks. the back-end server ignores the content-length header on requests to some endpoints.

The official solution confirms: Probe for vulnerable endpoints From the Proxy &gt; HTTP history, send the GET / request to Burp Repeater twice.

The root cause is a failure in the application's security architecture specific to this request smuggling scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab is vulnerable to CL.0 request smuggling attacks. The back-end server ignores the Content-Le"
- Reject requests with both Content-Length and Transfer-Encoding headers.
