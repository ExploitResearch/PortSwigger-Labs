# HTTP/2 request smuggling via CRLF injection

**Lab URL:** https://portswigger.net/web-security/request-smuggling/advanced/lab-request-smuggling-h2-request-smuggling-via-crlf-injection

### Goal -

Solve the PortSwigger lab: HTTP/2 request smuggling via CRLF injection

### Exploitation

1. Identify the smuggling variant (CL.TE, TE.CL, TE.TE, H2.CL, etc.)
2. Craft a smuggled request that will be processed by the back-end server
3. The smuggled request can bypass front-end security controls, capture other users' requests, or poison the cache

### Why It Works

This lab is vulnerable to request smuggling because the front-end server downgrades HTTP/2 requests and fails to adequately sanitize incoming headers.

### Key Takeaways

- This lab demonstrates using the front-end server downgrades HTTP/2 requests and fails to adequately sanitize incoming headers.
