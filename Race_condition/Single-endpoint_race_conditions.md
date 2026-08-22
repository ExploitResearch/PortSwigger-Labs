# Single-endpoint race conditions

**Lab URL:** https://portswigger.net/web-security/race-conditions/lab-race-conditions-single-endpoint

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

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Race_condition/images/77dcf0547b26_001.png)

In here, we can purchase some items.

**Login as user **`wiener`**:**

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Race_condition/images/77dcf0547b26_002.png)

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Race_condition/images/77dcf0547b26_003.png)

In the profile page, we can update our own email address.

**Try to update it:**

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Race_condition/images/77dcf0547b26_004.png)

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Race_condition/images/77dcf0547b26_005.png)

**Burp Suite HTTP history:**

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Race_condition/images/77dcf0547b26_006.png)

When we clicked the “Update email” button, it’ll send a POST request to `/my-account/change-email`, with parameter `email` and `csrf`.

After that, it’ll show a message that telling us **go to our email to confirm the change of e-mail**.

**Email client:**

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Race_condition/images/77dcf0547b26_007.png)

- Confirm link endpoint: `/confirm-email?user=wiener&token=Q5jCBYgZvCSPhWvF`

**Click on it:**

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Race_condition/images/77dcf0547b26_008.png)

**Refresh our profile page:**

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Race_condition/images/77dcf0547b26_009.png)

In the confirm link endpoint (`/confirm-email`), it has 2 GET parameters - `user` and `token`.

Hmm… **What if I can retrieve **`carlos@ginandjuice.shop`**’s confirm email token via race condition, more specially, it’s single-endpoint race condition…**

Sending parallel requests with different values to a single endpoint can sometimes trigger powerful race conditions.

Consider a password reset mechanism that stores the user ID and reset token in the user’s session.

In this scenario, sending two parallel password reset requests from the same session, but with two different usernames, could potentially cause the following collision:

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Race_condition/images/77dcf0547b26_010.png)

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

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Race_condition/images/77dcf0547b26_011.png)

As you can see, it redirected us to the login page. Which means **the change email function is tied to our session**.

**Next, we can try to change email address to **`carlos@ginandjuice.shop`** and the test one in the normal way:**

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Race_condition/images/77dcf0547b26_012.png)

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Race_condition/images/77dcf0547b26_013.png)

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Race_condition/images/77dcf0547b26_014.png)

As expected, we can only read the test one confirm email.

**Now, what if I send those requests in parallel?**

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Race_condition/images/77dcf0547b26_015.png)

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Race_condition/images/77dcf0547b26_016.png)

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Race_condition/images/77dcf0547b26_017.png)

**Oh! We won the race! Let’s click the confirm email link!**

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Race_condition/images/77dcf0547b26_018.png)

**Then refresh our profile page:**

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Race_condition/images/77dcf0547b26_019.png)

Nice! We now have administrator privilege!

**Let’s delete user **`carlos`**:**

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Race_condition/images/77dcf0547b26_020.png)

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Race_condition/images/77dcf0547b26_021.png)

## Conclusion

What we’ve learned:

1. Single-endpoint race conditions
