# JWT Summary Test cases

1. **Is it possible to use incorrectly signed (or modified) tokens? **
You can just tamper with the data leaving the signature as is and check if the server is checking the signature. Try to change your username to "admin”

---

1. **Modify the algorithm to None
**[**JWT authentication bypass via flawed signature verification**](https://app.notion.com/p/78b4034beaf14ee5a95b5deab13fbc04)** **
Set the algorithm used as "None" and remove the signature part.

---

1. **Origin(Generation of Token)**
It's important to determine whether the token was generated server-side or client-side by examining the proxy's request history.

  - Tokens first seen from the client side suggest the key might be exposed to client-side code, necessitating further investigation.
  - Tokens originating server-side indicate a secure process.

---

1. **Duration (How long is the token valid?)**
Check if the token lasts more than 24h... maybe it never expires. If there is a "exp" field, check if the server is correctly handling it.

Depending on the application:

▪ 30 minutes for high risk applications

▪ 60 minutes otherwise

---

1. **Brute-force HMAC secret**
  1. [JWT authentication bypass via weak signing key](https://app.notion.com/p/f82d109eed5e4e6696fc34299a786809) 
  1. [**See this page.**](https://book.hacktricks.xyz/generic-methodologies-and-resources/brute-force#jwt)

---

1. **Change the algorithm RS256(asymmetric) to HS256(symmetric) (CVE-2016-5431/CVE-2016-10555)**
The algorithm HS256 uses the secret key to sign and verify each message.
The algorithm RS256 uses the private key to sign the message and uses the public key for authentication.

If you change the algorithm from RS256 to HS256, the back end code uses the public key as the secret key and then uses the HS256 algorithm to verify the signature.

You can retrieve the certificate of the web server executing this:

```bash
openssl s_client -connect example.com:443 2>&1 < /dev/null | sed -n '/-----BEGIN/,/-----END/p' > certificatechain.pem #For this attack you can use the JOSEPH Burp extension. In the Repeater, select the JWS tab and select the Key confusion attack. Load the PEM, Update the request and send it. (This extension allows you to send the "none" algorithm attack also). It is also recommended to use the tool jwt_tool with the option 2 as the previous Burp Extension does not always works well.
openssl x509 -pubkey -in certificatechain.pem -noout > pubkey.pem
```

---

1. **New public key inside the header**
An attacker embeds a new key in the header of the token and the server uses this new key to verify the signature (CVE-2018-0114).

This can be done with the "JSON Web Tokens" Burp extension.
(Send the request to the Repeater, inside the JSON Web Token tab select "CVE-2018-0114" and send the request).

  - Embed your newly created RSA public key as JWK header
  - Instead of embedding public keys directly using the `jwk` header parameter, some servers let you use the `jku`(JWK Set URL) header parameter to reference a JWK Set containing the key. When verifying the signature, the server fetches the relevant key from this URL.

In the header of the JWT, replace the current value of the `kid` parameter with the `kid` of the JWK that you uploaded to the exploit server.
Add a new `jku` parameter to the header of the JWT. Set its value to the URL of your JWK Set on your exploit server where you host the public key as
```perl
{
    "keys": [
    <<PASTE PUBLIC key as JWK>>
    ]
}
```

However, it fails to check whether the provided URL belongs to a trusted domain before fetching the key.

  - An attacker could potentially **force the server to use an arbitrary file from its filesystem as the verification key**.
To do so, we can point the `kid `parameter to a predictable, static file, then sign the JWT using a secret that matches the contents of this file. For example, in Linux, `/dev/null `is an empty file, fetching it returns null. Therefore, signing the token with a Base64 encoded null byte will result in a valid signature.
