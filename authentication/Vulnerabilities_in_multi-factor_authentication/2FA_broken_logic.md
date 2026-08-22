# 2FA broken logic

- With Burp running, log in to your own account and investigate the 2FA verification process. Notice that in the `POST /login2` request, the `verify` parameter is used to determine which user's account is being accessed.
- Log out of your account.
- Send the `GET /login2` request to Burp Repeater. Change the value of the `verify` parameter to `carlos` and send the request. This ensures that a temporary 2FA code is generated for Carlos.
- Go to the login page and enter your username and password. Then, submit an invalid 2FA code.
- Send the `POST /login2` request to Burp Intruder.
- In Burp Intruder, set the `verify` parameter to `carlos` and add a payload position to the `mfa-code` parameter. Brute-force the verification code.
- Load the 302 response in the browser.
- Click **My account** to solve the lab.

generate verification code list

```bash
crunch 4 4 0123456789 -o todelete.txt
```

use turbo intruder

[https://www.hackingarticles.in/burp-suite-for-pentester-turbo-intruder/](https://www.hackingarticles.in/burp-suite-for-pentester-turbo-intruder/)

### Why It Works

The exploit succeeds because this lab's two-factor authentication is vulnerable due to its flawed logic. to solve the lab, access carlos's account page.

The official solution confirms: With Burp running, log in to your own account and investigate the 2FA verification process. Notice that in the POST /login2 request, the verify parame

The root cause is a failure in the application's security architecture specific to this authentication scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab's two-factor authentication is vulnerable due to its flawed logic. To solve the lab, access"
- Consistent error messages and rate-limiting prevent enumeration and brute-force.

## PortSwigger Lab

**Official lab:** 2FA broken logic

**PortSwigger:** https://portswigger.net/web-security/authentication/multi-factor/lab-2fa-broken-logic
