# Multi-endpoint race conditions

### Goal - 

 Purchase a **Lightweight L33t Leather Jacket**.

### Analysis/Exploitation -

{% hint style="success" %}
**Tip: **When experimenting, we recommend purchasing the gift card as you can later redeem this to avoid running out of store credit.
{% endhint %}


## Enumeration

![](./images/1458121b3c44_001.png)

**Login as user **`wiener`**:**

In the home page, we can purchase **gift cards, **Let’s try to buy 1:

**Then, we can go to our profile page to redeem the gift card:**

In Burp Suite HTTP history:

When we clicked the “Redeem” button, it’ll send a POST request to `/gift-card` with parameter `csrf` and `gift-card`. After successful redeem, it’ll redirect us back to `/my-account`, which is our profile page.

**If **`/gift-card` endpoint **has vulnerability, we can abuse that to gain infinite amount of store credit**!

Let’s test for race condition vulnerability!

Now, what if we send the multiple `/gift-card` POST request to redeem the same gift-card code more than once

**On “Send group in sequence (separate connections)” and “Send group in sequence (single connections)” options:**

It behaved as expected. In the first request, the gift card is redeemed, and the rest of the request shouldn’t able to redeem it again. It respond “Invalid gift card”. So **it’s validating the gift card**.

**On "Send group in parallel" option:**

It behaved Same… Maybe `/gift-card` POST endpoint doesn’t vulnerable to race condition?

![](./images/1458121b3c44_002.png)

![](./images/1458121b3c44_003.png)

Here we tried race condition at single endpoint but the lab name itself indicates that its vulnerable to Multi-endpoint race condition. 

How about **the process of buying gift cards**?

**In there, we can test for hidden multi-step sequences in POST endpoint **`/cart`** and **`/cart/checkout`**.**

In practice, a single request may initiate an entire multi-step sequence behind the scenes, transitioning the application through multiple hidden states that it enters and then exits again before request processing is complete. We’ll refer to these as “sub-states”.

If you can identify one or more HTTP requests that cause an interaction with the same data, you can potentially abuse these sub-states to expose time-sensitive variations of the kinds of logic flaws that are common in multi-step workflows. This enables race condition exploits that go far beyond limit overruns.

For example, you may be familiar with flawed multi-factor authentication (MFA) workflows that let you perform the first part of the login using known credentials, then navigate straight to the application via forced browsing, effectively bypassing MFA entirely.

The following pseudo-code demonstrates how a website could be vulnerable to a race variation of this attack:

```python
    session['userid'] = user.userid
    if user.mfa_enabled:
        session['enforce_mfa'] = True        # generate and send MFA code to user        # redirect browser to MFA code entry form
```

As you can see, this is in fact a multi-step sequence within the span of a single request. Most importantly, it transitions through a sub-state in which the user temporarily has a valid logged-in session, but MFA isn’t yet being enforced. An attacker could potentially exploit this by sending a login request along with a request to a sensitive, authenticated endpoint.

To detect and exploit hidden multi-step sequences, we recommend the following methodology, which is summarized from the whitepaper [Smashing the state machine: The true potential of web race conditions](https://portswigger.net/research/smashing-the-state-machine) by PortSwigger Research.

![](./images/1458121b3c44_004.png)

**1 - Predict potential collisions:**

Testing every endpoint is impractical. After mapping out the target site as normal, you can reduce the number of endpoints that you need to test by asking yourself the following questions:

- **Is this endpoint security critical?** Many endpoints don’t touch critical functionality, so they’re not worth testing.
- **Is there any collision potential?** For a successful collision, you typically need two or more requests that trigger operations on the same record. For example, consider the following variations of a password reset implementation:

![](./images/1458121b3c44_005.png)

With the first example, requesting parallel password resets for two different users is unlikely to cause a collision as it results in changes to two different records. However, the second implementation enables you to edit the same record with requests for two different users.

Perhaps the most intuitive form of these race conditions are those that involve sending requests to multiple endpoints at the same time.

Think about the classic logic flaw in online stores where you add an item to your basket or cart, pay for it, then add more items to the cart before force-browsing to the order confirmation page.

A variation of this vulnerability can occur when payment validation and order confirmation are performed during the processing of a single request. The state machine for the order status might look something like this:

![](./images/1458121b3c44_006.png)

In this case, you can potentially add more items to your basket during the race window between when the payment is validated and when the order is finally confirmed.

**Now, what if I added another gift card while checkout, what will happened?**

- **Test for under normal conditions:**

![](./images/1458121b3c44_007.png)

![](./images/1458121b3c44_008.png)

![](./images/1458121b3c44_009.png)

Working as expected, purchased a gift card, and another gift card is added to the basket.

- **Single-packet attack:**

![](./images/1458121b3c44_010.png)

Nope. No addition gift card order is being placed.

**Aligning multi-endpoint race windows:**

When testing for multi-endpoint race conditions, you may encounter issues trying to line up the race windows for each request, even if you send them all at exactly the same time using the single-packet technique.

![](./images/1458121b3c44_011.png)

This common problem is primarily caused by the following two factors:

- **Delays introduced by network architecture -** For example, there may be a delay whenever the front-end server establishes a new connection to the back-end. The protocol used can also have a major impact.
- **Delays introduced by endpoint-specific processing -** Different endpoints inherently vary in their processing times, sometimes significantly so, depending on what operations they trigger.

Fortunately, there are potential workarounds to both of these issues.

**Connection warming:**

Back-end connection delays don’t usually interfere with race condition attacks because they typically delay parallel requests equally, so the requests stay in sync.

It’s essential to be able to distinguish these from delays from those caused by endpoint-specific factors. One way to do this is by “warming” the connection with one or more inconsequential requests to see if this smoothes out the remaining processing times. In Burp Repeater, you can try adding a `GET` request for the homepage to the start of your tab group, then using the **Send group in sequence (single connection)** option.

If the first request still has a longer processing time, but the rest of the requests are now processed within a short window, you can ignore the apparent delay and continue testing as normal.

If you still see inconsistent response times on a single endpoint, even when using the single-packet technique, this is an indication that the back-end delay is interfering with your attack. You may be able to work around this by using Turbo Intruder to send some connection warming requests before following up with your main attack requests.

- **Perform connection warming:**

![](./images/1458121b3c44_012.png)

![](./images/1458121b3c44_013.png)

![](./images/1458121b3c44_014.png)

As you can see, in `/cart` POST endpoint, it took a lot longer than the `/checkout` endpoint. Which means this delay is caused by the back-end network architecture rather than the respective processing time of the each endpoint. Therefore, it is not likely to interfere with our attack.

**After some trial and error, when we try to purchase an item that we don’t have enough store credit, it’ll redirect us to **`/cart?err=INSUFFICIENT_FUNDS`**:**

![](./images/1458121b3c44_015.png)

Hmm… I wonder **what if we can bypass that restriction**…

**So, if I have 1 gift card in the basket (Any items that fits well with our store credit), then place the order, add an item that exceeds our store credit, and finally place the order again. Will that bypass the restriction and purchase the insufficient store credit item?**

- Create 2 groups:

**Group 1 - Buy jacket:**

![](./images/1458121b3c44_016.png)

![](./images/1458121b3c44_017.png)

**Group 2 - Buy gift card:**

![](./images/1458121b3c44_018.png)

![](./images/1458121b3c44_019.png)

- Keep sending both groups in parallel until the restriction has been bypassed:

![](./images/1458121b3c44_020.png)

Nice! We successfully bypassed the restriction!

## Conclusion

What we’ve learned:

1. Multi-endpoint race conditions
