# Server-side pause-based request smuggling

**Lab URL:** https://portswigger.net/web-security/request-smuggling/browser/pause-based-desync/lab-server-side-pause-based-request-smuggling

### Goal -

Solve the PortSwigger lab: Server-side pause-based request smuggling

### Exploitation

1. Identify the smuggling variant (CL.TE, TE.CL, TE.TE, H2.CL, etc.)
2. Craft a smuggled request that will be processed by the back-end server
3. The smuggled request can bypass front-end security controls, capture other users' requests, or poison the cache

### Why It Works

This lab is vulnerable to pause-based server-side request smuggling.

### Key Takeaways

- This lab is vulnerable to pause-based server-side request smuggling.
