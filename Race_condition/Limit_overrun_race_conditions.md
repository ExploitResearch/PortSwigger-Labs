# Limit overrun race conditions        

**Lab URL:** https://portswigger.net/web-security/race-conditions/lab-race-conditions-limit-overrun

### Goal - 

 Purchase a **Lightweight L33t Leather Jacket**.

### Analysis/Exploitation -

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Race_condition/images/e7e7c62b1122_001.png)

In home page, we can see that the promotion code `PROMO20` for 20% off, and we can purchase some items.

**Login as user** `wiener`**:**

Now, let's try to purchase the "Lightweight L33t Leather Jacket":

**Apply the coupon code** `PROMO20`**:**

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Race_condition/images/e7e7c62b1122_002.png)

When we clicked the "Apply" button, it'll send a POST request to `/cart/coupon`, with parameter `csrf` and `coupon`.

We still do not have enough store credit for this purchase after applying coupon.

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Race_condition/images/e7e7c62b1122_003.png)

If we try to apply the coupon again, it show an error message **"Coupon already applied"**:

In our case, the race window is the time of checking the coupon has been applied or not.

**To exploit this limit overruns race condition:**

1. Remove the applied coupon first
1. Then send the `/cart/coupon` POST request to Burp Suite's Repeater 30 times 
1. Add those tabs to group
1. Select "Send group in parallel"
1. After that, send the requests in parallel

The coupon reduced the original price a lot more! Therefore, the application's apply coupon function is indeed vulnerable to limit overruns race condition!

Now Place the order to solve the lab

### Why It Works

This lab's purchasing flow contains a race condition that enables you to purchase items for an unintended price.

### Key Takeaways

- This lab's purchasing flow contains a race condition that enables you to purchase items for an unintended price.
