# Flawed enforcement of business rules

### Goal - 

Exploit logic flaw to buy the Lightweight l33t leather jacket.

### Analysis/Exploitation 

**Login as user **`wiener`**:**

In here, we can see that **there is a code: **`NEWCUST5`** to get a legit discount for new customer:**

![](./images/7e7135bd2a53_001.png)

Let’s try to buy the leather jacket and apply the `NEWCUST5` coupon:

Now the total price is reduced by 5 dollars! Unfortunately, even with the discount, the jacket is still above  my store credit

Try to apply the coupon again but this does not work:

![](./images/7e7135bd2a53_002.png)

After poking around the web site, I found that there is a newsletter subscription at the very bottom of the page, sign up for a newsletter since subscriptions often contain nice offers.

![](./images/7e7135bd2a53_003.png)

When signing up for it, a Javascript popup appears with coupon, now we have 1 more coupon! `SIGNUP30`

![](./images/7e7135bd2a53_004.png)

After I apply it, the total price looks better than before. But still not affordable with the store credit available:

Try applying the code`SIGNUP30`, it is rejected because the coupon has already been applied but if we apply `NEWCUST5` it get acceped.

So if you enter the same code twice in a row, it is rejected However, if you alternate between the two codes, you can bypass this control. It looks like the 'is-the-discount-code-alread-used' check is only done with the latest discount code applied. So try to alternate the discounts until the price is** **below** **`$100.00`

![](./images/7e7135bd2a53_005.png)

Now `Place order`

### Why It Works

The exploit succeeds because this lab has a logic flaw in its purchasing workflow. to solve the lab, exploit this flaw to buy a &quot;lightweight l33t leather jacket&quot;.

The official solution confirms: Log in and notice that there is a coupon code, NEWCUST5. At the bottom of the page, sign up to the newsletter. You receive another coupon code, SIGNUP

The root cause is a failure in the application's security architecture specific to this logic flaws scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab has a logic flaw in its purchasing workflow. To solve the lab, exploit this flaw to buy a &"
- Validate business-critical parameters server-side — never trust client-supplied values.

## PortSwigger Lab

**Official lab:** Flawed enforcement of business rules

**PortSwigger:** https://portswigger.net/web-security/logic-flaws/examples/lab-logic-flaws-flawed-enforcement-of-business-rules
