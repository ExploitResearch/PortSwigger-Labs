# Client-side desync

### Goal -

Solve the PortSwigger lab: Client-side desync

### Exploitation

1. Identify the smuggling variant (CL.TE, TE.CL, TE.TE, H2.CL, etc.)
2. Craft a smuggled request that will be processed by the back-end server
3. The smuggled request can bypass front-end security controls, capture other users' requests, or poison the cache

### Why It Works

The exploit succeeds because this lab is vulnerable to client-side desync attacks because the server ignores the content-length header on requests to some endpoints. you can exploit this to induce a victim's browser to disclose i

The official solution confirms: Identify a vulnerable endpoint Notice that requests to / result in a redirect to /en.

The root cause is a failure in the application's security architecture specific to this request smuggling scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab is vulnerable to client-side desync attacks because the server ignores the Content-Length h"
- Reject requests with both Content-Length and Transfer-Encoding headers.

## PortSwigger Lab

**Official lab:** Client-side desync

**PortSwigger:** https://portswigger.net/web-security/request-smuggling/browser/client-side-desync/lab-client-side-desync
