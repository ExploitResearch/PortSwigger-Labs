# JWT authentication bypass via algorithm confusion with no exposed key

### Goal -

Exploit an algorithm confusion vulnerability in JWT verification when the server's public key is not directly exposed.

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

The server's JWT library accepts both RS256 and HS256 algorithms. When the attacker signs a JWT with HS256 using the server's RSA public key as the HMAC secret, the server verifies it using HMAC with the same public key. This allows the attacker to forge valid JWTs without knowing the RSA private key.

### Key Takeaways

- Pin the JWT algorithm to RS256 only (do not accept HS256)
- Never use the same key for different algorithm types
- Use a library that prevents algorithm confusion
- Do not expose public keys unnecessarily
