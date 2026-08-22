# JWT authentication bypass via kid header path traversal

**Lab URL:** https://portswigger.net/web-security/jwt/lab-jwt-authentication-bypass-via-kid-header-path-traversal

## Goal - 

Forge a JWT that gives you access to the admin panel at `/admin`, then delete the user `carlos`.

## Analysis/Exploitation -

**Login as user **`wiener`**:**

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/JWT_attack/images/c1d1d36c8c1c_001.png)

As you can see, in the header’s `alg`, it’s using an algorithm called HS256(HMAC + SHA-256), which is a [symmetric algorithm](https://portswigger.net/web-security/jwt/algorithm-confusion#symmetric-vs-asymmetric-algorithms).

**In the lab’s background, it said:**

{% hint style="info" %}
In order to verify the signature, the server uses the kid parameter in JWT header to fetch the relevant key from its filesystem.
{% endhint %}

{% hint style="info" %}
💡 An attacker could potentially **force the server to use an arbitrary file from its filesystem as the verification key**.

To do so, we can point the `kid `parameter to a predictable, static file, then sign the JWT using a secret that matches the contents of this file. For example, in Linux, `/dev/null `is an empty file, fetching it returns null. Therefore, signing the token with a Base64 encoded null byte will result in a valid signature.

{% endhint %}

### <span style="color: #337EA9">**Generate a suitable signing key**</span>

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/JWT_attack/images/c1d1d36c8c1c_002.png)

### <span style="color: #337EA9">**Modify and sign the JWT**</span>

- Modify payload’s `sub` claim to `administrator`:
- Modify header’s `kid` claim to a directory traversal payload, which point to `/dev/null`:
- sign with generated key symmetric key

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/JWT_attack/images/c1d1d36c8c1c_003.png)

Copy the JWT and update session cookie in the browser**, then refresh the page:**

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/JWT_attack/images/c1d1d36c8c1c_004.png)

go to the admin panel and delete user `carlos`
