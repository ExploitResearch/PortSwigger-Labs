# Web Cache Poisoning

Web cache poisoning exploits cache implementation flaws to serve malicious cached content to other users. Unlike cache deception (which tricks the cache into storing private data), cache poisoning injects malicious content INTO the cache that is then served to victims.

**Key concepts:**
- **Unkeyed inputs**: Headers, cookies, or parameters that affect the response but are not part of the cache key
- **Cache key**: The set of request components used to identify cached responses
- **Fat GET**: Adding a body to a GET request to influence the response

## Contents

- [Web cache poisoning with an unkeyed header](./Web_cache_poisoning_with_an_unkeyed_header.md)
- [Web cache poisoning with an unkeyed cookie](./Web_cache_poisoning_with_an_unkeyed_cookie.md)
- [Web cache poisoning with multiple headers](./Web_cache_poisoning_with_multiple_headers.md)
- [Targeted web cache poisoning using an unknown header](./Targeted_web_cache_poisoning_using_an_unknown_header.md)
- [Web cache poisoning via an unkeyed query string](./Web_cache_poisoning_via_an_unkeyed_query_string.md)
- [Web cache poisoning via an unkeyed query parameter](./Web_cache_poisoning_via_an_unkeyed_query_parameter.md)
- [Parameter cloaking](./Parameter_cloaking.md)
- [Web cache poisoning via a fat GET request](./Web_cache_poisoning_via_a_fat_GET_request.md)
- [URL normalization](./URL_normalization.md)
- [Web cache poisoning to exploit a DOM vulnerability via a cached page](./Web_cache_poisoning_to_exploit_a_DOM_vulnerability_via_a_cached_page.md)
- [Combining web cache poisoning vulnerabilities](./Combining_web_cache_poisoning_vulnerabilities.md)
- [Cache key injection](./Cache_key_injection.md)
- [Internal cache poisoning](./Internal_cache_poisoning.md)
