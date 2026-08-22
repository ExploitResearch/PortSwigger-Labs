# Response queue poisoning via H2.TE request smuggling

**Lab URL:** https://portswigger.net/web-security/request-smuggling/advanced/response-queue-poisoning/lab-request-smuggling-h2-response-queue-poisoning-via-te-request-smuggling

### Goal -

Solve the PortSwigger lab: Response queue poisoning via H2.TE request smuggling

### Exploitation

1. Identify the smuggling variant (CL.TE, TE.CL, TE.TE, H2.CL, etc.)
2. Craft a smuggled request that will be processed by the back-end server
3. The smuggled request can bypass front-end security controls, capture other users' requests, or poison the cache
