# CORS

## Contents

- [CORS vulnerability with basic origin reflection](./CORS_vulnerability_with_basic_origin_reflection/README.md)
- [CORS vulnerability with trusted null origin](./CORS_vulnerability_with_trusted_null_origin/README.md)
- [CORS vulnerability with trusted insecure protocols](./CORS_vulnerability_with_trusted_insecure_protocols/README.md)
- [CORS vulnerability with internal network pivot attack](./CORS_vulnerability_with_internal_network_pivot_attack/README.md)

### CORS

CORS allows controlled access to resources located outside of a given domain by relaxing the same-origin policy for trusted domains. It provides a way for servers to specify which origins (domains, ports, schemes) are allowed to access their resources. This is done through HTTP headers sent by the server in response to requests from other origins. These headers tell the browser which origins are permitted to access the resources, allowing the server to control access to its data and APIs.

While CORS is a security feature that helps prevent unauthorized requests from other domains, it does not protect against all cross-origin attacks, such as cross-site request forgery (CSRF). Poorly configured CORS policies can create potential vulnerabilities, leading to cross-domain attacks. Therefore, it's essential for web developers and administrators to properly configure and implement CORS policies to ensure the security of their web applications.

  - **CORS Request Flow**:
    - When a web page hosted on one domain makes a request to a resource (e.g., an API endpoint) hosted on another domain, the browser sends an HTTP request with an "Origin" header indicating the origin of the requesting page.
    - The server then examines this Origin header to determine if the requesting domain is allowed to access the resource.
    - If the server approves the request, it responds with additional CORS headers, such as "Access-Control-Allow-Origin", indicating which origins are allowed to access the resource.
    - If the request is denied, the browser prevents the web page from accessing the response data, enforcing the SOP.
### [Same-origin policy (SOP)](https://portswigger.net/web-security/cors/same-origin-policy)

The same-origin policy is a restrictive cross-origin specification that limits the ability for a website to interact with resources outside of the source domain. The same-origin policy was defined many years ago in response to potentially malicious cross-domain interactions, such as one website stealing private data from another. It generally allows a domain to issue requests to other domains, but not to access the responses.

An origin consists of a combination of protocol (e.g., HTTP), domain (e.g., [example.com](http://example.com/)), and port (e.g., 80).

### Relaxation of the same-origin policy

The same-origin policy is very restrictive and consequently various approaches have been devised to circumvent the constraints. Many websites interact with subdomains or third-party sites in a way that requires full cross-origin access. A controlled relaxation of the same-origin policy is possible using cross-origin resource sharing (CORS).

The cross-origin resource sharing protocol uses a suite of HTTP headers that define trusted web origins and associated properties such as whether authenticated access is permitted. Browsers permit access to responses to cross-origin requests based upon these header instructions. 


The `Access-Control-Allow-Origin` header is included in the response from one website to a request originating from another website, and identifies the permitted origin of the request. A web browser compares the Access-Control-Allow-Origin with the requesting website's origin and permits access to the response if they match.
The default behavior of cross-origin resource requests is for requests to be passed without credentials like cookies and the Authorization header. However, the cross-domain server can permit reading of the response when credentials are passed to it by setting the CORS `Access-Control-Allow-Credentials` header to true. Now if the requesting website uses JavaScript to declare that it is sending cookies with the request:

### Relaxation of CORS specifications with wildcards

The header `Access-Control-Allow-Origin` supports wildcards. For example:

```text
Access-Control-Allow-Origin: *
```

> 💡 **NOTE:**

Wildcards cannot be used within any other value. For example, the following header is **not** valid:

```text
Access-Control-Allow-Origin: https://*.normal-website.com
```

The use of the wildcard is restricted in the specification as you cannot combine the wildcard with the cross-origin transfer of credentials (authentication, cookies or client-side certificates). Consequently, a cross-domain server response of the form: 

```text
Access-Control-Allow-Origin: *
Access-Control-Allow-Credentials: true
```

is not permitted as this would be dangerously insecure, exposing any authenticated content on the target site to everyone.

### **CORS Headers**:

    - **Access-Control-Allow-Origin**: Specifies which origins are allowed to access the resource. It can be set to a specific origin, "*", or a list of origins.
    - **Access-Control-Allow-Credentials**: Indicates whether the browser should include credentials (such as cookies) in CORS requests.
    - **Access-Control-Allow-Methods**: Specifies the HTTP methods (e.g., GET, POST, PUT, DELETE) allowed when accessing the resource.
    - **Access-Control-Allow-Headers**: Specifies which headers can be used in the actual request.
    - **Access-Control-Expose-Headers**: Specifies which headers can be exposed to the browser in the response.
**Preflight Requests**:

      - Preflight requests are used for certain types of cross-origin requests, such as those that use methods other than GET, POST, or HEAD, or those that use custom headers.
      - Before sending the actual request, the browser sends an OPTIONS preflight request to the server to determine if the actual request is safe to send.
      - The server responds to the preflight request with appropriate CORS headers, indicating whether the actual request is allowed.
**Simple Requests**:

      - Simple requests are those that meet certain criteria, such as using only safe methods (GET, POST, HEAD) and not including custom headers beyond a few common ones.
      - For simple requests, the browser automatically adds the necessary CORS headers to the request, and no preflight request is needed.

### **How to prevent CORS-based attacks**

### Only allow trusted sites

It may seem obvious but origins specified in the `Access-Control-Allow-Origin` header should only be sites that are trusted. In particular, dynamically reflecting origins from cross-origin requests without validation is readily exploitable and should be avoided.

### Avoid whitelisting null

Avoid using the header `Access-Control-Allow-Origin: null`. Cross-origin resource calls from internal documents and sandboxed requests can specify the `null` origin. CORS headers should be properly defined in respect of trusted origins for private and public servers.

### Avoid wildcards in internal networks

Avoid using wildcards in internal networks. Trusting network configuration alone to protect internal resources is not sufficient when internal browsers can access untrusted external domains.


