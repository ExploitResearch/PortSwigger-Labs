# Web cache poisoning via HTTP/2 request tunnelling

### Goal -

Solve the PortSwigger lab: Web cache poisoning via HTTP/2 request tunnelling

### Exploitation

1. Identify the smuggling variant (CL.TE, TE.CL, TE.TE, H2.CL, etc.)
2. Craft a smuggled request that will be processed by the back-end server
3. The smuggled request can bypass front-end security controls, capture other users' requests, or poison the cache

### Why It Works

The exploit succeeds because this lab is vulnerable to request smuggling because the front-end server downgrades http/2 requests and doesn't consistently sanitize incoming headers.

The official solution confirms: Send a request for GET / to Burp Repeater. Expand the Inspector's Request Attributes section and make sure the protocol is set to HTTP/2. Using the In

The root cause is a failure in the application's security architecture specific to this request smuggling scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab is vulnerable to request smuggling because the front-end server downgrades HTTP/2 requests "
- Reject requests with both Content-Length and Transfer-Encoding headers.
