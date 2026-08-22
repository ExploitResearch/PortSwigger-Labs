# Web Cache Poisoning

Web cache poisoning exploits cache implementation flaws to serve malicious cached content to other users. Unlike cache deception (which tricks the cache into storing private data), cache poisoning injects malicious content INTO the cache that is then served to victims.

**Key concepts:**
- **Unkeyed inputs**: Headers, cookies, or parameters that affect the response but are not part of the cache key
- **Cache key**: The set of request components used to identify cached responses
- **Fat GET**: Adding a body to a GET request to influence the response
