# Parameter cloaking

### Goal -

Solve the PortSwigger lab: Parameter cloaking

### Vulnerability / Concept

Web cache poisoning exploits unkeyed inputs - request components that influence the response but are not included in the cache key. By manipulating these inputs, an attacker can cause the cache to store a poisoned response that is served to all subsequent users requesting that cache key.

### Recon / Initial Analysis

1. Identify caching behavior (response headers like `X-Cache`, `Age`, `Cache-Control`)
2. Identify unkeyed inputs by varying headers, cookies, and parameters
3. Check if the response changes based on these unkeyed inputs
4. Look for DOM-based vulnerabilities in cached pages

### Exploitation

1. Identify unkeyed headers or parameters that affect the response
2. Craft a request with the malicious unkeyed input
3. Submit the request to poison the cache
4. Verify that subsequent normal requests receive the poisoned response

### Why It Works

The cache uses a subset of request components (the cache key) to identify cached responses. If an input is unkeyed but affects the response, the cache may store a response generated from a malicious request and serve it to all users who request the same cache key.

### Key Takeaways

- Include all response-affecting inputs in the cache key
- Use `Vary` header to specify which headers affect caching
- Avoid caching responses with user-specific content
- Test for unkeyed headers, cookies, and parameters
