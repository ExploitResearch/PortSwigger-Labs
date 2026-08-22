# Bypassing access controls via HTTP/2 request tunnelling

**Lab URL:** https://portswigger.net/web-security/request-smuggling/advanced/request-tunnelling/lab-request-smuggling-h2-bypass-access-controls-via-request-tunnelling

### Goal -

Solve the PortSwigger lab: Bypassing access controls via HTTP/2 request tunnelling

### Exploitation

1. Identify the smuggling variant (CL.TE, TE.CL, TE.TE, H2.CL, etc.)
2. Craft a smuggled request that will be processed by the back-end server
3. The smuggled request can bypass front-end security controls, capture other users' requests, or poison the cache
