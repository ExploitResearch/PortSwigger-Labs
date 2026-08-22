# JWT authentication bypass via algorithm confusion with no exposed key

**Lab URL:** https://portswigger.net/web-security/jwt/algorithm-confusion/lab-jwt-authentication-bypass-via-algorithm-confusion-with-no-exposed-key

### Goal -

Exploit an algorithm confusion vulnerability in JWT verification when the server's public key is not directly exposed.

### Exploitation

1. Identify that the server accepts JWTs and uses RS256
2. Check for exposed public keys (JWKS endpoint, /.well-known/jwks.json, certificate endpoints)
3. Obtain the server's RSA public key
4. Convert the public key to PEM format
5. Sign a JWT using HS256 with the PEM-encoded public key as the HMAC secret
6. Modify the JWT payload (e.g., change `sub` to `administrator`)
7. Submit the forged JWT
