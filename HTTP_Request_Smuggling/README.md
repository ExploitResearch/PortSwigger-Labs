# HTTP Request Smuggling

HTTP request smuggling is a technique that exploits differences in how front-end (proxy/load balancer) and back-end servers interpret HTTP requests. By crafting ambiguous requests, an attacker can 'smuggle' a hidden request past the front-end server, where it is processed by the back-end as part of the next user's request.

**Key concepts:**

- **CL.TE**: Front-end uses Content-Length, back-end uses Transfer-Encoding
- **TE.CL**: Front-end uses Transfer-Encoding, back-end uses Content-Length
- **TE.TE**: Both servers support Transfer-Encoding but one can be bypassed via obfuscation
- **HTTP/2 smuggling**: Exploits HTTP/2-specific features like CRLF injection in headers
- **Client-side desync**: The browser is tricked into sending smuggled requests to the back-end

## Labs

- [0CL request smuggling](./0CL_request_smuggling.md)
- [Bypassing access controls via HTTP2 request tunnelling](./Bypassing_access_controls_via_HTTP2_request_tunnelling.md)
- [CL0 request smuggling](./CL0_request_smuggling.md)
- [H2CL request smuggling](./H2CL_request_smuggling.md)
- [HTTP2 request smuggling via CRLF injection](./HTTP2_request_smuggling_via_CRLF_injection.md)
- [HTTP2 request splitting via CRLF injection](./HTTP2_request_splitting_via_CRLF_injection.md)
- [HTTP request smuggling basic CLTE vulnerability](./HTTP_request_smuggling_basic_CLTE_vulnerability.md)
- [HTTP request smuggling basic TECL vulnerability](./HTTP_request_smuggling_basic_TECL_vulnerability.md)
- [HTTP request smuggling confirming a CLTE vulnerability via timing techniques](./HTTP_request_smuggling_confirming_a_CLTE_vulnerability_via_timing_techniques.md)
- [HTTP request smuggling confirming a TECL vulnerability via timing techniques](./HTTP_request_smuggling_confirming_a_TECL_vulnerability_via_timing_techniques.md)
- [HTTP request smuggling via CRLF injection into the Host header](./HTTP_request_smuggling_via_CRLF_injection_into_the_Host_header.md)
- [Web cache poisoning via HTTP2 request tunnelling](./Web_cache_poisoning_via_HTTP2_request_tunnelling.md)
