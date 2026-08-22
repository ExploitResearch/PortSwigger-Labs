# Flawed enforcement of business rules

**Lab URL:** https://portswigger.net/web-security/logic-flaws/examples/lab-logic-flaws-flawed-enforcement-of-business-rules

### Goal - 

Exploit logic flaw to buy the Lightweight l33t leather jacket.

### Analysis/Exploitation 

**Login as user **`wiener`**:**

In here, we can see that **there is a code: **`NEWCUST5`** to get a legit discount for new customer:**

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Business_logic_vulnerabilities/images/7e7135bd2a53_001.png)

Let’s try to buy the leather jacket and apply the `NEWCUST5` coupon:

Now the total price is reduced by 5 dollars! Unfortunately, even with the discount, the jacket is still above  my store credit

Try to apply the coupon again but this does not work:

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Business_logic_vulnerabilities/images/7e7135bd2a53_002.png)

After poking around the web site, I found that there is a newsletter subscription at the very bottom of the page, sign up for a newsletter since subscriptions often contain nice offers.

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Business_logic_vulnerabilities/images/7e7135bd2a53_003.png)

When signing up for it, a Javascript popup appears with coupon, now we have 1 more coupon! `SIGNUP30`

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Business_logic_vulnerabilities/images/7e7135bd2a53_004.png)

After I apply it, the total price looks better than before. But still not affordable with the store credit available:

Try applying the code`SIGNUP30`, it is rejected because the coupon has already been applied but if we apply `NEWCUST5` it get acceped.

So if you enter the same code twice in a row, it is rejected However, if you alternate between the two codes, you can bypass this control. It looks like the 'is-the-discount-code-alread-used' check is only done with the latest discount code applied. So try to alternate the discounts until the price is** **below** **`$100.00`

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Business_logic_vulnerabilities/images/7e7135bd2a53_005.png)

Now `Place order`

### Why It Works

This lab has a logic flaw in its purchasing workflow.

### Key Takeaways

- This lab has a logic flaw in its purchasing workflow.
