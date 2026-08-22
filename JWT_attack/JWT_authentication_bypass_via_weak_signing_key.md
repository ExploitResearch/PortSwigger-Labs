# JWT authentication bypass via weak signing key

**Lab URL:** https://portswigger.net/web-security/jwt/lab-jwt-authentication-bypass-via-weak-signing-key

## Goal - 

First brute-force the website’s secret key. Once you’ve obtained this, use it to sign a modified session token that gives you access to the admin panel at `/admin`, then delete the user `carlos`.

## Analysis/Exploitation -

**Login as user **`wiener`**:**

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/JWT_attack/images/f82d109eed5e_001.png)

In Burp Proxy we can see, the algorithm is HS256(HMAC + SHA-256), which uses an arbitrary, standalone string as the secret key.

So, **what if we know the secret key**? If we know that, **we can create JWTs with any header and payload values, then use the key to re-sign the token with a valid signature!**

## <span style="color: #BE5B00">**Find the secret key:**</span>

<span style="color: #337EA9">**Using Hashcat**</span>

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/JWT_attack/images/f82d109eed5e_002.png)

 [wordlist of common secret keys](https://github.com/wallarm/jwt-secrets/blob/master/jwt.secrets.list).      

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/JWT_attack/images/f82d109eed5e_003.png)

After a short time, hashcat is successful in finding the correct key: **secret1**

<span style="color: #337EA9">**Using JohnTheRipper**</span>

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/JWT_attack/images/f82d109eed5e_004.png)

I already cracked the password earlier so we can use **—show **to view previously hacked passwords with John The Ripper
`john --show hashed_passwords.txt`

## <span style="color: #BE5B00">Generate valid signature:</span>

now can **use the secret key to generate a valid signature for any JWT header and payload**!

<span style="color: #337EA9">**Using **</span>[<span style="color: #337EA9">**jwt.io**</span>](https://jwt.io/)

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/JWT_attack/images/f82d109eed5e_005.png)

<span style="color: #337EA9">**Using JWT editor**</span>

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/JWT_attack/images/f82d109eed5e_006.png)

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/JWT_attack/images/f82d109eed5e_007.png)

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/JWT_attack/images/f82d109eed5e_008.png)

Now that I know that the JWT is correct for `administrator`, I can replace my session cookie with this manipulated token. That way, I do not need to modify requests but can work directly in the browser.

**Let’s copy and paste that newly generated JWT string to our session cookie:**

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/JWT_attack/images/f82d109eed5e_009.png)

**Then refresh the page : **go to the admin panel and delete user `carlos`

go to the admin panel and delete user `carlos`
