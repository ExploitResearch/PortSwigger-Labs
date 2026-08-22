# JWT authentication bypass via unverified signature

**Lab URL:** https://portswigger.net/web-security/jwt/lab-jwt-authentication-bypass-via-unverified-signature

### Goal - 

Modify your session token to gain access to the admin panel at `/admin`, then delete the user `carlos`.

### Analysis/Exploitation -

As the lab application deals with JWTs, Use the extension `JSON Web Tokens (JWT4B)` or `JWT Editor `to avoid having to deal with manual decoding and encoding of the JWTs all the time.

**Login as user **`wiener`

Burp Proxy notifies me that the response contains a JWT and highlight it.

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/JWT_attack/images/0efb99ed06f3_001.png)

In the header part, the signature’s algorithm is RS256(RSA + SHA-256), and it has a kid(Key ID). 
In the payload part, it has an issuer(`portswigger`), subject(`wiener`), and expires(`1710394513`).

When I try to access the `/admin` page as user `wiener`, I am greeted by the message `Admin interface only available if logged in as an administrator`.

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/JWT_attack/images/0efb99ed06f3_002.png)

**Now, in the lab’s background, it said:**

{% hint style="info" %}
Due to implementation flaws, the server doesn’t verify the signature of any JWTs that it receives.

**To check **Does the website verify the signature? and Accepting arbitrary signatures

**we can just simply modify payload’s subject to **`administrator`**:**

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/JWT_attack/images/0efb99ed06f3_003.png)

**To delete user carlos we can use any of following ways:**

1. Send the request to `/admin/delete?username=carlo`
1. copy the modified cookie value from the request and replace the cookie in browser:

1. use Burp "Match and Replace" functionality to replace the cookie, or even the specific claim, on the fly for all requests. However, just changing the cookie in the browser is much simpler.
{% endhint %}
