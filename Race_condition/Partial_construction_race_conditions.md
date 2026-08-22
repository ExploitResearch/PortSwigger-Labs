# Partial construction race conditions

To solve the lab:

1. Identify the vulnerability in the way the website generates password reset tokens.
1. Obtain a valid password reset token for the user `carlos`.
1. Log in as `carlos`.
1. Access the admin panel and delete the user `carlos`.

You can log into your account with the following credentials: `wiener:peter`.

{% hint style="info" %}
Note:

Solving this lab requires Burp Suite 2023.9 or higher.

{% endhint %}


## Enumeration

**Home page:**

![](./images/d2355c7081f1_001.png)

In this web application, we can read different blog posts.

**Login page:**

![](./images/d2355c7081f1_002.png)

**What’s that “Forgot password?” link?**

![](./images/d2355c7081f1_003.png)

We can reset a user’s password!

**Let’s try **`wiener`** first and see what will happen:**

![](./images/d2355c7081f1_004.png)

![](./images/d2355c7081f1_005.png)

**Burp Suite HTTP history:**

![](./images/d2355c7081f1_006.png)

When we clicked the “Submit” button, it’ll send a POST request to `/forgot-password` with `csrf` and `username` parameter.

**Email client:**

![](./images/d2355c7081f1_007.png)

We can go to the reset password endpoint to enter our new password!

**Reset password endpoint **`/forgot-password?user=<username_here>&token=<token_here>`**.**

Let’s go there!

![](./images/d2355c7081f1_008.png)

In here, we can type our new password and change the old one.

**Time-sensitive attacks:**

Sometimes you may not find race conditions, but the techniques for delivering requests with precise timing can still reveal the presence of other vulnerabilities.

One such example is when high-resolution timestamps are used instead of cryptographically secure random strings to generate security tokens.

Consider a password reset token that is only randomized using a timestamp. In this case, it might be possible to trigger two password resets for two different users, which both use the same token. All you need to do is time the requests so that they generate the same timestamp.

Hmm… I wonder what’s that password reset token.

**It looks like a hashed string, we can try to identify the hash algorithm via **`hashid`**:**

```text
┌[siunam♥Mercury]-(~/ctf/Portswigger-Labs)-[2023.09.25|14:15:54(HKT)]
└> hashid '38b7357daa3f78c8f607dd539a06a2a1ecdc96df'
Analyzing '38b7357daa3f78c8f607dd539a06a2a1ecdc96df'
[+] SHA-1
[+] Double SHA-1
[+] RIPEMD-160
[+] Haval-160
[+] Tiger-160
[+] HAS-160
[+] LinkedIn
[+] Skein-256(160)
[+] Skein-512(160)
```

Oh! It’s SHA-1 hash!

I’m also curious about **what’s the original string before hashed**?

Maybe it’s based on **timestamp**?

To test that, we can **send the generate token request (**`POST /forgot-password`**) in parallel.**

**First, let’s try send that request in separate connections:**

![](./images/d2355c7081f1_009.png)

![](./images/d2355c7081f1_010.png)

As you can see, the tokens are different.

**How about send in parallel?**

![](./images/d2355c7081f1_011.png)

![](./images/d2355c7081f1_012.png)

They’re still different?

**Then, I noticed that there’s a delay between the requests:**

![](./images/d2355c7081f1_013.png)

![](./images/d2355c7081f1_014.png)

That being said, our requests are being ***processed in sequence rather than concurrently***.

Also, in our session cookie name `phpsessionid`, it’s suggested that **the backend is using PHP**.

**Session-based locking mechanisms:**

Some frameworks attempt to prevent accidental data corruption by using some form of request locking. For example, PHP’s native session handler module only processes one request per session at a time.

It’s extremely important to spot this kind of behavior as it can otherwise mask trivially exploitable vulnerabilities. If you notice that all of your requests are being processed sequentially, try sending each of them using a different session token.

**To solve our requests are being processed one request per session at a time, we can use a different session token:**

![](./images/d2355c7081f1_015.png)

![](./images/d2355c7081f1_016.png)

{% hint style="info" %}
Note: Remember to retrieve the CSRF token.

**Then, in our Burp Suite’s Repeater tab, replace the original session token cookie and CSRF token to a request tab:**

![](./images/d2355c7081f1_017.png)

![](./images/d2355c7081f1_018.png)

**Next, send those requests in parallel and check the password reset token in our email client:**

![](./images/d2355c7081f1_019.png)

Nice!! We got the same password reset token!!
{% endhint %}

{% hint style="info" %}
Note: Sometimes it may fails, you could send those requests a couple more times.
{% endhint %}


## Exploitation

Armed with above information, it’s clear that **the password reset token is generated via timestamp and SHA-1 hashed.**

**To perform account takeover on user **`carlos`**, we can simply change the **`username`** POST parameter to **`carlos`** in one of our Repeater’s requests:**

![](./images/d2355c7081f1_020.png)

![](./images/d2355c7081f1_021.png)

**Then, send those requests and get the password reset token, which should be the same as the **`carlos`** one.**

![](./images/d2355c7081f1_022.png)

**Finally, send a POST request to **`/forgot-password?user=carlos&token=<token_here>`** with POST parameter **`csrf`**, **`token`**, **`user`**, **`new-password-1`**, and **`new-password-2`** to reset **`carlos`**’s password:**

![](./images/d2355c7081f1_023.png)

**Now, we should be able to login as user **`carlos`**:**

![](./images/d2355c7081f1_024.png)

![](./images/d2355c7081f1_025.png)

**Nice! Let’s go to the admin panel and delete user **`carlos`**!**

![](./images/d2355c7081f1_026.png)

![](./images/d2355c7081f1_027.png)

## Conclusion

What we’ve learned:

1. Exploiting time-sensitive vulnerabilities

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab contains a user registration mechanism. A race condition enables you to bypass email verification and register with an arbitrary email address that you do not own."

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

An attacker could bypass rate limits and brute-force protections, apply discount codes multiple times, withdraw money multiple times, create duplicate accounts, bypass one-time-use restrictions, or exploit TOCTOU vulnerabilities in file operations.

### Detection / Testing Methodology

1. Identify endpoints that perform state-changing operations (purchases, transfers, redemptions)
2. Test for rate limiting by sending concurrent requests
3. Use Burp Repeater or Turbo Intruder for parallel requests
4. Check for single-use restrictions that can be bypassed via race conditions
5. Test multi-endpoint race conditions (partial construction)
6. Look for TOCTOU vulnerabilities in file operations

### Remediation

- Implement proper database transactions with appropriate isolation levels
- Use pessimistic locking (SELECT FOR UPDATE) for critical resources
- Implement optimistic concurrency control (version checks)
- Use atomic operations for state changes
- Rate-limit critical endpoints
- Design for idempotency where possible

### Key Takeaways

- This lab demonstrates a race conditions vulnerability in a real-world scenario.
- The vulnerability occurs because user input reaches a sensitive operation without proper validation.
- The PortSwigger lab confirms: "This lab contains a user registration mechanism. A race condition enables you to bypass email verifi"
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Implement proper database transactions with appropriate isolation levels
