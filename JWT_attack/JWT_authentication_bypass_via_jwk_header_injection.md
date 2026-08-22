# JWT authentication bypass via jwk header injection

## Goal - 

Modify and sign a JWT that gives you access to the admin panel at `/admin`, then delete the user `carlos`.

## Analysis/Exploitation -

**Login as user **`wiener`**:**

![](./images/c3406da85f24_001.png)

In the header’s `alg`, it tells that **it’s using RS256(RSA + SHA-256) algorithm.**

**In the lab’s background, it said:**

{% hint style="info" %}
The server supports the jwk(JSON Web Key) parameter in the JWT header. This is sometimes used to embed the correct verification key directly in the token. However, it fails to check whether the provided key came from a trusted source.
{% endhint %}

To exploit that, we can sign a modified JWT using our own RSA private key, then embedding the matching public key in the `jwk` header.

<span style="color: #337EA9">Generate a new RSA key pair:</span>

![](./images/c3406da85f24_002.png)

<span style="color: #337EA9">Embedding the matching public key in the </span><span style="color: #337EA9">`jwk`</span><span style="color: #337EA9"> header:</span>

Send the post-login `GET /my-account?id=wiener` request to Burp Repeater, then remove id parameter                  

![](./images/c3406da85f24_003.png)

{% hint style="info" %}
💡 If the request contains an invalid or no JWT as the session cookie, the application redirects to the `/login` page.
{% endhint %}

I send the request and the response contains my account page, confirming that the signature verification on the backend used the RSA public key information I injected in the JWT header.

![](./images/c3406da85f24_004.png)

Change the `sub` value of the token to `administrator`, perform the `Attack -> Embedd JWK` option again

![](./images/c3406da85f24_005.png)

Copy the JWT and update session cookie in the browser**, and refresh the page:**

go to the admin panel and delete user `carlos`

## PortSwigger Lab

**Official lab:** JWT authentication bypass via jwk header injection

**PortSwigger:** https://portswigger.net/web-security/jwt/lab-jwt-authentication-bypass-via-jwk-header-injection
