# HTTP Host Header Attacks

HTTP Host header attacks exploit applications that trust the `Host` header without validation. The `Host` header specifies which website the client is accessing, but when servers use it for routing, password reset links, or cache keys without proper validation, attackers can manipulate it to bypass security controls.

## Contents

- [Basic password reset poisoning](./Basic_password_reset_poisoning.md)
- [Host header authentication bypass](./Host_header_authentication_bypass.md)
- [Web cache poisoning via ambiguous requests](./Web_cache_poisoning_via_ambiguous_requests.md)
- [Routing-based SSRF](./Routing-based_SSRF.md)
- [SSRF via flawed request parsing](./SSRF_via_flawed_request_parsing.md)
- [Host validation bypass via connection state attack](./Host_validation_bypass_via_connection_state_attack.md)
- [Password reset poisoning via dangling markup](./Password_reset_poisoning_via_dangling_markup.md)
