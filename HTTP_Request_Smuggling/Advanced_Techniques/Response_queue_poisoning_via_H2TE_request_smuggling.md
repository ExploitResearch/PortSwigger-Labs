# Response queue poisoning via H2.TE request smuggling

### Goal -

Solve the PortSwigger lab: Response queue poisoning via H2.TE request smuggling

### Exploitation

1. Identify the smuggling variant (CL.TE, TE.CL, TE.TE, H2.CL, etc.)
2. Craft a smuggled request that will be processed by the back-end server
3. The smuggled request can bypass front-end security controls, capture other users' requests, or poison the cache

### Why It Works

The exploit succeeds because this lab is vulnerable to request smuggling because the front-end server downgrades http/2 requests even if they have an ambiguous length.

The official solution confirms: Using Burp Repeater, try smuggling an arbitrary prefix in the body of an HTTP/2 request using chunked encoding as follows. Remember to expand the Insp

The root cause is a failure in the application's security architecture specific to this request smuggling scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab is vulnerable to request smuggling because the front-end server downgrades HTTP/2 requests "
- Reject requests with both Content-Length and Transfer-Encoding headers.

## PortSwigger Lab

**Official lab:** Response queue poisoning via H2.TE request smuggling

**PortSwigger:** https://portswigger.net/web-security/request-smuggling/advanced/response-queue-poisoning/lab-request-smuggling-h2-response-queue-poisoning-via-te-request-smuggling
