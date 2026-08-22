# JWT authentication bypass via flawed signature verification

### Goal - 

Modify your session token to gain access to the admin panel at `/admin`, then delete the user `carlos`.


### Vulnerability / Concept

JSON Web Token (JWT) vulnerabilities arise when applications improperly verify or handle JWT signatures. JWTs consist of three parts: header, payload, and signature. Common flaws include accepting unsigned tokens, not verifying the signature algorithm, allowing algorithm confusion (RS256 to HS256), and trusting user-controlled header parameters like `jwk`, `jku`, and `kid`.

JWTs are stateless — the server doesn't store session data, it trusts the token's contents based on the signature. If signature verification is flawed, an attacker can forge tokens with arbitrary claims (e.g., changing `sub` to `administrator` or `role` to `admin`).

### Recon / Initial Analysis

1. Identify if the application uses JWTs (check cookies, Authorization headers, URL parameters)
2. Decode the JWT (base64) to examine the header (alg, kid, typ) and payload (sub, role, exp)
3. Check if the signature is verified — modify the payload and resubmit
4. Test if the `alg` header can be changed (e.g., RS256 → HS256, none)
5. Look for exposed public keys (JWKS endpoints, certificate files, /.well-known)
6. Check if `jwk`, `jku`, or `kid` header parameters are processed
7. Test if weak signing keys can be brute-forced (hashcat -m 16500)

### Analysis/Exploitation -

**Login as user **`wiener`**:**

![](./images/78b4034beaf1_001.png)

Burp Proxy notifies me that the response contains a JWT and highlight it.

When I try to access the `/admin` page as user `wiener`, I am greeted by the message `Admin interface only available if logged in as an administrator`.

![](./images/78b4034beaf1_002.png)

**in the lab’s background, it said:**

{% hint style="info" %}
The server is insecurely configured to accept unsigned JWTs.

To check Does the website trust the algorithm specified in the token? and **Accepting tokens with no signature**

**Change the header’s **`alg`**(algorithm) to **`none`**:**
{% endhint %}

{% hint style="info" %}
💡 remove the signature from the JWT, but remember to leave the trailing dot after the payload.

![](./images/78b4034beaf1_003.png)

We are still logged-in as wiener, This confirms that the backend trusts and uses the algorithm provided in the token to provide access to authenticated content.

**let’s change the payload’s **`sub`** to **`administrator`**:**so that we get authenticated as administrator

![](./images/78b4034beaf1_004.png)

**copy and paste the newly modified JWT  to our session cookie:**

![](./images/78b4034beaf1_005.png)

Refresh the page, go to admin panel and delete user carlos

![](./images/78b4034beaf1_006.png)
{% endhint %}

### Why It Works

The server's JWT verification is flawed — it either doesn't verify the signature, accepts unsigned tokens, allows algorithm switching, or trusts user-supplied keys via header parameters. The core issue is a broken trust boundary: the server trusts the token's claims without properly verifying that the token was issued by the authentication server.

In algorithm confusion, the server's library accepts both RS256 (asymmetric) and HS256 (symmetric). When the attacker signs with HS256 using the server's RSA public key as the HMAC secret, the server verifies using HMAC with the same public key — accepting a forged token without the private key.

### Real-World Impact

An attacker could:
- Forge admin tokens to gain full administrative access
- Impersonate any user by modifying the `sub` claim
- Bypass authentication entirely by using `alg: none`
- Escalate privileges by modifying `role` or `isAdmin` claims
- Access other users' data and perform actions on their behalf
- Bypass expiration by modifying the `exp` claim

### Remediation

- Pin the JWT algorithm to a single expected value (e.g., RS256 only)
- Never accept `alg: none` or unsigned tokens
- Use a well-maintained JWT library that prevents algorithm confusion
- Do not process user-controlled `jwk`, `jku`, or `kid` header parameters
- Use strong, random signing keys (256-bit minimum)
- Store keys securely and rotate them regularly
- Implement server-side session revocation despite JWT statelessness

### Key Takeaways

- Never trust JWT claims without verifying the signature with the correct algorithm and key.
- Algorithm confusion (RS256→HS256) is a critical flaw — always pin the expected algorithm.
- User-controlled JWT header parameters (`jwk`, `jku`, `kid`) are injection points for attacks.
- Weak signing keys can be brute-forced offline — use strong, random secrets.
- The `alg: none` attack works when the library doesn't explicitly reject unsigned tokens.
