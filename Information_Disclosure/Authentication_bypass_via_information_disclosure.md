# Authentication bypass via information disclosure

### Goal - 

Access the admin interface and delete the user `carlos`.

### Analysis/Exploitation -

After browsing around a bit and logging in with the known credentials, nothing too interesting appears. Time to check the requests in Burp. Nothing too interesting there either.

The admin endpoint in some previous labs was found under `/admin`. But to avoid using this knowledge, I can use multiple means of content discovery. Burp Professional comes with such functionality and several good free tools allow for content discovery as well.

The one I use here is [ffuf](https://github.com/ffuf/ffuf) together with the great wordlists provided by [SecLists](https://github.com/danielmiessler/SecLists):

```html
ffuf -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-small.txt -u https://0aeb000b03ce98ffc09d247e001c00a4.web-security-academy.net/FUZZ
```

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Information_Disclosure/images/3beb0bad2d8c_001.png)

### Visiting the endpoint

On visiting this admin page it shows this message:

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Information_Disclosure/images/3beb0bad2d8c_002.png)

**It only allows local users, which is using the localhost(**`127.0.0.1`**) IP address.**

{% hint style="info" %}
💡 A common way of propagating originating IPs to a web server (used in proxy or load balancing scenarios) is the `X-Forwarded-For` header. This, however, does not work here (and the lab description states it is a custom header anyway).
{% endhint %}

Two HTTP methods can be used to obtain additional information, `OPTIONS` and `TRACE`. The latter produces an interesting result:

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Information_Disclosure/images/3beb0bad2d8c_003.png)

Notice that the `X-Custom-IP-Authorization` header, containing my IP address, was automatically appended to the request. This is used to determine whether or not the request came from the `localhost` IP address.                 

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Information_Disclosure/images/3beb0bad2d8c_004.png)

Now that I know the header, accessing the admin interface becomes easy. I need to ensure the custom header is sent with each request so I add a `Match and Replace` rule to always add this new header to requests.

I use `127.0.0.1` as the content to trick the application to believe that the request originated from `localhost`.

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Information_Disclosure/images/3beb0bad2d8c_005.png)

Now just reload the page in the browser, access the admin panel and delete user `carlos` to solve the lab:

### Why It Works

The exploit succeeds because this lab uses a jwt-based mechanism for handling sessions. it uses a robust rsa key pair to sign and verify tokens. however, due to implementation flaws, this mechanism is vulnerable to algorithm conf

The root cause is a failure in the application's security architecture specific to this jwt scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab uses a JWT-based mechanism for handling sessions. It uses a robust RSA key pair to sign and"
- JWT signature verification must pin the algorithm and reject unsigned tokens.

## PortSwigger Lab

**Official lab:** Authentication bypass via information disclosure

**PortSwigger:** https://portswigger.net/web-security/information-disclosure/exploiting/lab-infoleak-authentication-bypass
