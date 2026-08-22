# HTTP Request Smuggling

HTTP request smuggling is a technique that exploits differences in how front-end (proxy/load balancer) and back-end servers interpret HTTP requests. By crafting ambiguous requests, an attacker can 'smuggle' a hidden request past the front-end server, where it is processed by the back-end as part of the next user's request.

**Key concepts:**

- **CL.TE**: Front-end uses Content-Length, back-end uses Transfer-Encoding
- **TE.CL**: Front-end uses Transfer-Encoding, back-end uses Content-Length
- **TE.TE**: Both servers support Transfer-Encoding but one can be bypassed via obfuscation
- **HTTP/2 smuggling**: Exploits HTTP/2-specific features like CRLF injection in headers
- **Client-side desync**: The browser is tricked into sending smuggled requests to the back-end

## Contents

- [HTTP request smuggling, basic CL.TE vulnerability](./HTTP_request_smuggling_basic_CLTE_vulnerability.md)
- [HTTP request smuggling, basic TE.CL vulnerability](./HTTP_request_smuggling_basic_TECL_vulnerability.md)
- [HTTP request smuggling, obfuscating the TE header](./HTTP_request_smuggling_obfuscating_the_TE_header.md)
- [HTTP request smuggling, confirming a CL.TE vulnerability via timing techniques](./HTTP_request_smuggling_confirming_a_CLTE_vulnerability_via_timing_techniques.md)
- [HTTP request smuggling, confirming a TE.CL vulnerability via timing techniques](./HTTP_request_smuggling_confirming_a_TECL_vulnerability_via_timing_techniques.md)
- [Exploiting HTTP request smuggling to bypass front-end security controls](./Exploiting_HTTP_request_smuggling_to_bypass_front-end_security_controls.md)
- [Exploiting HTTP request smuggling to reveal front-end request rewriting](./Exploiting_HTTP_request_smuggling_to_reveal_front-end_request_rewriting.md)
- [Exploiting HTTP request smuggling to capture other users' requests](./Exploiting_HTTP_request_smuggling_to_capture_other_users_requests.md)
- [Exploiting HTTP request smuggling to deliver reflected XSS](./Exploiting_HTTP_request_smuggling_to_deliver_reflected_XSS.md)
- [Response queue poisoning via H2.TE request smuggling](./Response_queue_poisoning_via_H2TE_request_smuggling.md)
- [H2.CL request smuggling](./H2CL_request_smuggling.md)
- [HTTP/2 request smuggling via CRLF injection](./HTTP2_request_smuggling_via_CRLF_injection.md)
- [HTTP/2 request splitting via CRLF injection](./HTTP2_request_splitting_via_CRLF_injection.md)
- [0.CL request smuggling](./0CL_request_smuggling.md)
- [CL.0 request smuggling](./CL0_request_smuggling.md)
- [Exploiting HTTP request smuggling to perform web cache poisoning](./Exploiting_HTTP_request_smuggling_to_perform_web_cache_poisoning.md)
- [Exploiting HTTP request smuggling to perform web cache deception](./Exploiting_HTTP_request_smuggling_to_perform_web_cache_deception.md)
- [Bypassing access controls via HTTP/2 request tunnelling](./Bypassing_access_controls_via_HTTP2_request_tunnelling.md)
- [Web cache poisoning via HTTP/2 request tunnelling](./Web_cache_poisoning_via_HTTP2_request_tunnelling.md)
- [Client-side desync](./Client-side_desync.md)
- [Server-side pause-based request smuggling](./Server-side_pause-based_request_smuggling.md)
- [HTTP request smuggling via CRLF injection into the Host header](./HTTP_request_smuggling_via_CRLF_injection_into_the_Host_header.md)
