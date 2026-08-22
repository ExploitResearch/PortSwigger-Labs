# HTTP/2 request splitting via CRLF injection

### Goal -

Solve the PortSwigger lab: HTTP/2 request splitting via CRLF injection

### Exploitation

1. Identify the smuggling variant (CL.TE, TE.CL, TE.TE, H2.CL, etc.)
2. Craft a smuggled request that will be processed by the back-end server
3. The smuggled request can bypass front-end security controls, capture other users' requests, or poison the cache

### Why It Works

The exploit succeeds because this lab is vulnerable to request smuggling because the front-end server downgrades http/2 requests and fails to adequately sanitize incoming headers.

The official solution confirms: Send a request for GET / to Burp Repeater. Expand the Inspector's Request Attributes section and make sure the protocol is set to HTTP/2. Change the p

The root cause is a failure in the application's security architecture specific to this request smuggling scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab is vulnerable to request smuggling because the front-end server downgrades HTTP/2 requests "
- Reject requests with both Content-Length and Transfer-Encoding headers.

## PortSwigger Lab

**Official lab:** HTTP/2 request splitting via CRLF injection

**PortSwigger:** https://portswigger.net/web-security/request-smuggling/advanced/lab-request-smuggling-h2-request-splitting-via-crlf-injection
