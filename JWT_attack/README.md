# JWT attack

## Contents

- [JWT authentication bypass via unverified signature](./JWT_authentication_bypass_via_unverified_signature/README.md)
- [JWT authentication bypass via flawed signature verification](./JWT_authentication_bypass_via_flawed_signature_verification/README.md)
- [JWT authentication bypass via weak signing key](./JWT_authentication_bypass_via_weak_signing_key/README.md)
- [JWT authentication bypass via jwk header injection](./JWT_authentication_bypass_via_jwk_header_injection/README.md)
- [JWT authentication bypass via jku header injection](./JWT_authentication_bypass_via_jku_header_injection/README.md)
- [JWT authentication bypass via kid header path traversal](./JWT_authentication_bypass_via_kid_header_path_traversal/README.md)
- [JWT authentication bypass via algorithm confusion](./JWT_authentication_bypass_via_algorithm_confusion/README.md)
- [JWT authentication bypass via algorithm confusion with no exposed key](./JWT_authentication_bypass_via_algorithm_confusion_with_no_exposed_key/README.md)
- [JWT Summary Test cases](./JWT_Summary_Test_cases/README.md)
- [JWT Security Testing/Penetration Testing Checklist](./JWT_Security_TestingPenetration_Testing_Checklist/README.md)

### JWT Tokens

JSON web tokens (JWTs) are a standardized format for sending cryptographically signed JSON data between systems. They can theoretically contain any kind of data, but are most commonly used to send information ("claims") about users as part of authentication, session handling, and access control mechanisms.  

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/daecbeb1-1197-4df0-8562-28e9ec26114a/45900f86-61c7-48bf-9d58-8b0cf1f6bae8.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466YC4ILEI5%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215625Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIF%2FycEFuRHIUqcpk3kFo6wwoaAHAlgaBfVDF4AaJveMAAiA%2FCTiWTrZtHV9%2FplZzulMYuAXWYq4h11g6MLPfDJ02RiqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMUrGf2lmBYYRjx0ZmKtwDf5uDrWoOy60tgVzeuj2XKjdOYWvhkIXRfF8RdX8XbBiKw3n1NMF71yEmAS3WFoIVk1WDKINDfKhloflMKiIy7ePBPZFUqPSD0Dgmy8CRQq0ZklkKfuI4G5Mb40%2BQudI%2BlqsMNntwgXGtl8%2FUSiXA9Poy63UNP7lFLc0m%2FcLnPxdfOekjwJByFteF1an2Rq9jZd%2BrpzpdQuJ5ekSfGoMpOxi%2BI1kEaEKJQQH9v2OWkYYDRpkvLthVuoRGenIs8giDUVyuaGX5Nppap6bafYL2ZHee6SHWgWCjyWp6HXd%2FH6ZoQIVMWXo4LanoDkSlWYLAu9uQFMVQ%2BNj%2F%2BLjf5wuYWxsWz%2BPf9vpqzXcesCttLM8wvYekxya4RNiqLw%2B1tXiqpgRV3Osr6fAQEVPJx1bC5zdhpLt4pwmApB2wUIAFY0C1S6VSo448UQxHN8fhZSvqnu9x4j%2FInbOuhZpfi3yT9ik8NScMucTQd87a2wP2olsA9PRrH258CnBqCUvj7au8%2FvcFfmcvTcsu7nr3jjOoKaMsMYuFGhGxN8lJ3N4svh0JKwazo8UNvbb9b07wy07mzLVSm6zpyKFUArnsToGwoEd2bQzPXxHBTZug0jC7tZickD7C6H%2BpBQy9FsQw1Iaj1AY6pgFieG7HtL1MmOfRZeOll7C8w1VnQH%2BRMxMSoi8AH7zDM32P3JmPEbw28NUhxd1p9Or0VbnjYPhdqMPlvOWaXA09DNKol6TmnIPxz5JvhpfYw4MqlXoSldUFWQxc1jxsaibF%2F2Vys1Dp8xqzVqiyUQ8k3Zwe4kPjZO5Xhp0y6b%2B7rCkbu6iZmtlVdlE9ZRZnUluCnZ43ASq9oN7SvWmZ4chsnd5pFshS&X-Amz-Signature=163d01f9a7651a467ca5e43f16f26da475e56dd91922f050c8ac7954c247af0f&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

JWTs consist of three parts: a header, a payload, and a signature. These are each separated by a dot, the structure of a JWT looks like this:

```text
xxxxxxxxxx.yyyyyyyyyy.zzzzzzzzzz
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/4f08393b-6fc8-4bde-a550-7d5212a22911/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466YC4ILEI5%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215625Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIF%2FycEFuRHIUqcpk3kFo6wwoaAHAlgaBfVDF4AaJveMAAiA%2FCTiWTrZtHV9%2FplZzulMYuAXWYq4h11g6MLPfDJ02RiqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMUrGf2lmBYYRjx0ZmKtwDf5uDrWoOy60tgVzeuj2XKjdOYWvhkIXRfF8RdX8XbBiKw3n1NMF71yEmAS3WFoIVk1WDKINDfKhloflMKiIy7ePBPZFUqPSD0Dgmy8CRQq0ZklkKfuI4G5Mb40%2BQudI%2BlqsMNntwgXGtl8%2FUSiXA9Poy63UNP7lFLc0m%2FcLnPxdfOekjwJByFteF1an2Rq9jZd%2BrpzpdQuJ5ekSfGoMpOxi%2BI1kEaEKJQQH9v2OWkYYDRpkvLthVuoRGenIs8giDUVyuaGX5Nppap6bafYL2ZHee6SHWgWCjyWp6HXd%2FH6ZoQIVMWXo4LanoDkSlWYLAu9uQFMVQ%2BNj%2F%2BLjf5wuYWxsWz%2BPf9vpqzXcesCttLM8wvYekxya4RNiqLw%2B1tXiqpgRV3Osr6fAQEVPJx1bC5zdhpLt4pwmApB2wUIAFY0C1S6VSo448UQxHN8fhZSvqnu9x4j%2FInbOuhZpfi3yT9ik8NScMucTQd87a2wP2olsA9PRrH258CnBqCUvj7au8%2FvcFfmcvTcsu7nr3jjOoKaMsMYuFGhGxN8lJ3N4svh0JKwazo8UNvbb9b07wy07mzLVSm6zpyKFUArnsToGwoEd2bQzPXxHBTZug0jC7tZickD7C6H%2BpBQy9FsQw1Iaj1AY6pgFieG7HtL1MmOfRZeOll7C8w1VnQH%2BRMxMSoi8AH7zDM32P3JmPEbw28NUhxd1p9Or0VbnjYPhdqMPlvOWaXA09DNKol6TmnIPxz5JvhpfYw4MqlXoSldUFWQxc1jxsaibF%2F2Vys1Dp8xqzVqiyUQ8k3Zwe4kPjZO5Xhp0y6b%2B7rCkbu6iZmtlVdlE9ZRZnUluCnZ43ASq9oN7SvWmZ4chsnd5pFshS&X-Amz-Signature=5396f29cbfe488f9ec145e5a2fcad69c7f871ca6d1646fe8f890288da9577fe0&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

The header and payload parts of a JWT are just base64url-encoded JSON objects.

  1. **Header:** The header typically consists of two parts: the type of the token (JWT) and the signing algorithm being used (e.g., HMAC SHA256 or RSA).It header contains metadata about the token itself
Example:

```json
{
  "alg": "HS256",
  "typ": "JWT"
}

```

  1. **Payload:** The second part of the token is the payload, which contains claims. Claims are statements about an entity (typically, the user) and additional data.
Example:

```json
{
  "sub": "1234567890",
  "name": "John Doe",
  "iat": 1516239022
}
```

Commonly used claims include "iss" (issuer), "exp" (expiration time), "sub" (subject), and more.

  1. **Signature:** To create the signature part, you have to take the encoded header, the encoded payload, a secret, the algorithm specified in the header, and sign that.
The server that issues the token typically generates the signature by hashing the header and payload. In some cases, they also encrypt the resulting hash. Either way, this process involves a secret signing key. This mechanism provides a way for servers to verify that none of the data within the token has been tampered with since it was issued:

    - As the signature is directly derived from the rest of the token, changing a single byte of the header or payload results in a mismatched signature.
    - Without knowing the server's secret signing key, it shouldn't be possible to generate the correct signature for a given header or payload.

Example (with HMAC SHA256):

```text
HMACSHA256(
  base64UrlEncode(header) + "." + base64UrlEncode(payload),
  secret
)
```

### How JWT Works:

  1. **Authentication:** When a user logs in, the server creates a JWT and sends it to the client.
  1. **Authorization:** The client includes the JWT in the headers of subsequent requests. This allows the server to verify the identity of the user and authorize access.
  1. **Information Exchange:** JWTs are often used to transmit information between parties in a secure manner.

### Use Cases:

  - **Authentication:** After a user logs in, the server can issue a JWT as a token of authentication.
  - **Information Exchange:** JWTs can be used to transmit information between different parts of an application or between different applications.

### Benefits:

  - **Compact and URL-Safe:** JWTs are small and can be sent as URL parameters.
  - **Self-Contained:** All the necessary information is contained within the token, reducing the need to query the database.
  - **Stateless:** JWTs are stateless, meaning servers don't need to store sessions.

### Security Considerations:

  - **Secure Transmission:** Use HTTPS to transmit JWTs to prevent interception.
  - **Token Expiry:** Include an expiration time (exp) in the payload to limit the lifespan of a token.
  - **Signature:** Sign the JWT with a secret key or a private key to ensure its integrity.

## What is the impact of JWT attacks?

The impact of JWT attacks is usually severe. If an attacker is able to create their own valid tokens with arbitrary values, they may be able to escalate their own privileges or impersonate other users, taking full control of their accounts.

### **JWT vs JWS vs JWE**

The JWT specification is actually very limited. It only defines a format for representing information ("claims") as a JSON object that can be transferred between two parties. In practice, JWTs aren't really used as a standalone entity. The JWT spec is extended by both the JSON Web Signature (JWS) and JSON Web Encryption (JWE) specifications, which define concrete ways of actually implementing JWTs. 

![](https://portswigger.net/web-security/jwt/images/jwt-jws-jwe.jpg)

 In other words, a JWT is usually either a JWS or JWE token. When people use the term "JWT", they almost always mean a JWS token. JWEs are very similar, except that the actual contents of the token are encrypted rather than just encoded. 

### Note

For simplicity, throughout these materials, "JWT" refers primarily to JWS tokens, although some of the vulnerabilities described may also apply to JWE tokens. 

Here's an analogy to understand the differences:

  - **Think of JWT as a sealed envelope:** It defines the format and structure of the envelope (header, payload)
but doesn't guarantee its contents haven't been tampered with.
  - **JWS adds a signature like a wax seal:** It verifies the envelope hasn't been opened and identifies the sender.
  - **JWE adds encryption like a lock:** It ensures only authorized recipients with the key can access the information inside the envelope.

### How do vulnerabilities to JWT attacks arise?

 By design, servers don't usually store any information about the JWTs that they issue. Instead, each token is an entirely self-contained entity. This has several advantages, but also introduces a fundamental problem - the server doesn't actually know anything about the original contents of the token, or even what the original signature was. Therefore, if the server doesn't verify the signature properly, there's nothing to stop an attacker from making arbitrary changes to the rest of the token. 

For example, consider a JWT containing the following claims:

```text
{
    "username": "carlos",
    "isAdmin": false
}
```

If the server identifies the session based on this `username`, modifying its value might enable an attacker to impersonate other logged-in users. Similarly, if the `isAdmin` value is used for access control, this could provide a simple vector for privilege escalation.

JWT vulnerabilities typically arise due to flawed JWT handling within the application itself. The [various specifications](https://portswigger.net/web-security/jwt#jwt-vs-jws-vs-jwe) related to JWTs are relatively flexible by design, allowing website  developers to decide many implementation details for themselves. This can result in them accidentally introducing vulnerabilities even when using battle-hardened libraries.

 These implementation flaws usually mean that the signature of the JWT is not verified properly. This enables an attacker to tamper with the values passed to the application via the token's payload. Even if the signature is robustly verified, whether it can truly be trusted relies heavily on the server's secret key remaining a secret. If this key is leaked in some way, or can be guessed or brute-forced, an attacker can generate a valid signature for any arbitrary token, compromising the entire mechanism. 
        

### JWT header parameter injections

According to the JWS specification, only the `alg `header parameter is mandatory. In practice, however, JWT headers (also known as JOSE headers) often contain several other parameters. The following ones are of particular interest to attackers.

  - `jwk` (JSON Web Key) - Provides an embedded JSON object representing the key.
The JSON Web Signature (JWS) specification describes an optional `jwk` header parameter, which servers can use to embed their public key directly within the token itself in JWK format.

> **JWK**

A JWK (JSON Web Key) is a standardized format for representing keys as a JSON object.

  - `jku` (JSON Web Key Set URL) - Provides a URL from which servers can fetch a set of keys containing the correct key.
Instead of embedding public keys directly using the `jwk` header parameter, some servers let you use the `jku `(JWK Set URL) header parameter to reference a JWK Set containing the key. When verifying the signature, the server fetches the relevant key from this URL.

> **JWK Set
**A JWK Set is a JSON object containing an array of JWKs representing different keys.

  - `kid` (Key ID) - Provides an ID that servers can use to identify the correct key in cases where there are multiple keys to choose from. Depending on the format of the key, this
may have a matching `kid` parameter.
Servers may use several cryptographic keys for signing different kinds of data, not just JWTs. For this reason, the header of a JWT may contain a `kid` (Key ID) parameter, which helps the server identify which key to use when verifying the signature.

As you can see, these user-controllable parameters each tell the recipient server which key to use when verifying the signature.

### Algorithm confusion attacks

Algorithm confusion attacks (also known as key confusion attacks) occur when an attacker is able to force the server to verify the signature of a JSON web token (JWT) using a different algorithm than is intended by the website's developers. If this case isn't handled properly, this may enable attackers to forge valid JWTs containing arbitrary values without needing to know the server's secret signing key. 
