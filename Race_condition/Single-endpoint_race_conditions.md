# Single-endpoint race conditions

## Background

This lab’s email change feature contains a race condition that enables you to associate an arbitrary email address with your account.

Someone with the address `carlos@ginandjuice.shop` has a pending invite to be an administrator for the site, but they have not yet created an account. Therefore, any user who successfully claims this address will automatically inherit admin privileges.

To solve the lab:

1. Identify a race condition that lets you claim an arbitrary email address.
1. Change your email address to `carlos@ginandjuice.shop`.
1. Access the admin panel.
1. Delete the user `carlos`

You can log in to your own account with the following credentials: `wiener:peter`.

You also have access to an email client, where you can view all emails sent to `@exploit-<YOUR-EXPLOIT-SERVER-ID>.exploit-server.net` addresses.

{% hint style="info" %}
Note
Solving this lab requires Burp Suite 2023.9 or higher.
{% endhint %}


## Enumeration

**Home page:**

![](./images/77dcf0547b26_001.png)

In here, we can purchase some items.

**Login as user **`wiener`**:**

![](./images/77dcf0547b26_002.png)

![](./images/77dcf0547b26_003.png)

In the profile page, we can update our own email address.

**Try to update it:**

![](./images/77dcf0547b26_004.png)

![](./images/77dcf0547b26_005.png)

**Burp Suite HTTP history:**

![](./images/77dcf0547b26_006.png)

When we clicked the “Update email” button, it’ll send a POST request to `/my-account/change-email`, with parameter `email` and `csrf`.

After that, it’ll show a message that telling us **go to our email to confirm the change of e-mail**.

**Email client:**

![](./images/77dcf0547b26_007.png)

- Confirm link endpoint: `/confirm-email?user=wiener&token=Q5jCBYgZvCSPhWvF`

**Click on it:**

![](./images/77dcf0547b26_008.png)

**Refresh our profile page:**

![](./images/77dcf0547b26_009.png)

In the confirm link endpoint (`/confirm-email`), it has 2 GET parameters - `user` and `token`.

Hmm… **What if I can retrieve **`carlos@ginandjuice.shop`**’s confirm email token via race condition, more specially, it’s single-endpoint race condition…**

Sending parallel requests with different values to a single endpoint can sometimes trigger powerful race conditions.

Consider a password reset mechanism that stores the user ID and reset token in the user’s session.

In this scenario, sending two parallel password reset requests from the same session, but with two different usernames, could potentially cause the following collision:

![](./images/77dcf0547b26_010.png)

Note the final state when all operations are complete:

- `session['reset-user'] = victim`
- `session['reset-token'] = 1234`

The session now contains the victim’s user ID, but the valid reset token is sent to the attacker.

{% hint style="info" %}
Note:

For this attack to work, the different operations performed by each process must occur in just the right order. It would likely require multiple attempts, or a bit of luck, to achieve the desired outcome.

{% endhint %}


Email address confirmations, or any email-based operations, are generally a good target for single-endpoint race conditions. Emails are often sent in a background thread after the server issues the HTTP response to the client, making race conditions more likely.

Since we don’t have control over the `carlos@ginandjuice.shop` email address, we could try to exploit single-endpoint race condition to read/overwrite `carlos`’s email confirm token.

## Exploitation

**Now, what if there’s no session cookie in the **`/my-account/change-email`** POST endpoint?**

![](./images/77dcf0547b26_011.png)

As you can see, it redirected us to the login page. Which means **the change email function is tied to our session**.

**Next, we can try to change email address to **`carlos@ginandjuice.shop`** and the test one in the normal way:**

![](./images/77dcf0547b26_012.png)

![](./images/77dcf0547b26_013.png)

![](./images/77dcf0547b26_014.png)

As expected, we can only read the test one confirm email.

**Now, what if I send those requests in parallel?**

![](./images/77dcf0547b26_015.png)

![](./images/77dcf0547b26_016.png)

![](./images/77dcf0547b26_017.png)

**Oh! We won the race! Let’s click the confirm email link!**

![](./images/77dcf0547b26_018.png)

**Then refresh our profile page:**

![](./images/77dcf0547b26_019.png)

Nice! We now have administrator privilege!

**Let’s delete user **`carlos`**:**

![](./images/77dcf0547b26_020.png)

![](./images/77dcf0547b26_021.png)

## Conclusion

What we’ve learned:

1. Single-endpoint race conditions

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab's email change feature contains a race condition that enables you to associate an arbitrary email address with your account."

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
- The PortSwigger lab confirms: "This lab's email change feature contains a race condition that enables you to associate an arbitrary"
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Implement proper database transactions with appropriate isolation levels
