# JWT authentication bypass via algorithm confusion with no exposed key

### Goal -

Exploit an algorithm confusion vulnerability in JWT verification when the server's public key is not directly exposed.


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

### Vulnerability / Concept

The server uses RSA for signing but accepts HS256 (HMAC) signed tokens. Without the public key being directly exposed, the attacker must find it through other means (e.g., a JWKS endpoint, certificate file, or by trying common keys).

### Exploitation

1. Identify that the server accepts JWTs and uses RS256
2. Check for exposed public keys (JWKS endpoint, /.well-known/jwks.json, certificate endpoints)
3. Obtain the server's RSA public key
4. Convert the public key to PEM format
5. Sign a JWT using HS256 with the PEM-encoded public key as the HMAC secret
6. Modify the JWT payload (e.g., change `sub` to `administrator`)
7. Submit the forged JWT

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
