# Client-side desync

**Lab URL:** https://portswigger.net/web-security/request-smuggling/browser/client-side-desync/lab-client-side-desync

### Goal -

Solve the PortSwigger lab: Client-side desync

### Exploitation

1. Identify the smuggling variant (CL.TE, TE.CL, TE.TE, H2.CL, etc.)
2. Craft a smuggled request that will be processed by the back-end server
3. The smuggled request can bypass front-end security controls, capture other users' requests, or poison the cache

### Why It Works

This lab is vulnerable to client-side desync attacks because the server ignores the Content-Length header on requests to some endpoints.

### Key Takeaways

- This lab demonstrates using the server ignores the Content-Length header on requests to some endpoints.
