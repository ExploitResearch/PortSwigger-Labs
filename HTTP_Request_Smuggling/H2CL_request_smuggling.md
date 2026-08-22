# H2.CL request smuggling

### Goal -

Solve the PortSwigger lab: H2.CL request smuggling

### Vulnerability / Concept

HTTP request smuggling exploits the difference between how front-end and back-end servers handle the boundary between HTTP requests. By sending a request with both `Content-Length` and `Transfer-Encoding` headers, the attacker can trick the servers into disagreeing about where one request ends and the next begins.

### Recon / Initial Analysis

1. Identify if the application uses a front-end/back-end architecture (proxy, load balancer)
2. Test for CL.TE and TE.CL vulnerabilities using timing techniques
3. Check if HTTP/2 is supported (for H2-based smuggling)
4. Identify if the front-end rewrites requests (for request capture attacks)

### Exploitation

1. Identify the smuggling variant (CL.TE, TE.CL, TE.TE, H2.CL, etc.)
2. Craft a smuggled request that will be processed by the back-end server
3. The smuggled request can bypass front-end security controls, capture other users' requests, or poison the cache

### Why It Works

The HTTP specification allows both `Content-Length` and `Transfer-Encoding` headers, but doesn't specify which takes precedence when both are present. Front-end and back-end servers may disagree on which header to use, creating an opportunity for the attacker to 'smuggle' a second request that the front-end doesn't see.

### Key Takeaways

- Always use HTTP/2 end-to-end to avoid CL/TE ambiguities
- Reject requests with both Content-Length and Transfer-Encoding
- Normalize HTTP/1.1 headers before forwarding
- Use strict request validation on both front-end and back-end
