# SSRF

## Contents

- [Basic SSRF against the local server](./Basic_SSRF_against_the_local_server/README.md)

### SSRF Explained: Server-Side Request Forgery

SSRF, which stands for **Server-Side Request Forgery**, is a web security vulnerability that allows attackers to manipulate a server into making unintended requests to internal resources or external systems. This can be used to steal sensitive data, perform unauthorized actions, or even gain complete control of the server.

**Here's how it works:**

  1. **Attacker finds vulnerable input:** The attacker identifies a part of the application where they can
control or modify user input that is used to construct URLs or perform
requests. This could be a search bar, image upload form, or any other functionality that accepts user input.
  1. **Crafting a malicious URL:** The attacker crafts a malicious URL that points to a resource they want the server to access. This could be an internal server file, a database endpoint, or even an external website containing sensitive information.
  1. **Server makes the request:** The server, unaware of the attacker's manipulation, uses the provided URL to make the request. This can happen because the server trusts the user input or has inadequate validation mechanisms.
  1. **Attacker gains access:** Depending on the accessed resource, the attacker can potentially:
    - **Leak sensitive data:** Internal file contents, database records, or other sensitive information might be exposed.
    - **Perform unauthorized actions:** The attacker might be able to manipulate internal systems or services.
    - **Gain server control:** In severe cases, the attacker could exploit vulnerabilities in the accessed resource to gain complete control of the server.

**Here are some common ways SSRF attacks are carried out:**

  - **IP addresses:** Attackers might use internal IP addresses or loopback addresses (e.g., 127.0.0.1) to access internal resources.
  - **Local file system:** Attackers might manipulate paths to access files on the server itself.
  - **External services:** Attackers might target external services with sensitive information or functionalities accessible by the server.

**Preventing SSRF attacks:**

  - **Validate user input:** Sanitize and validate all user-provided input before using it to construct URLs or make requests.
  - **Restrict internal access:** Only allow internal resources to be accessed by authorized users and processes.
  - **Whitelist allowed URLs:** Use a whitelist to restrict the server to only access pre-approved external URLs.
  - **Keep software updated:** Regularly update web server software and libraries to patch known vulnerabilities.