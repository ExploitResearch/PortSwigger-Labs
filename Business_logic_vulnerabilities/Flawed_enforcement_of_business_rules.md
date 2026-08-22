# Flawed enforcement of business rules

### Goal - 

Exploit logic flaw to buy the Lightweight l33t leather jacket.



### Vulnerability / Concept

This lab demonstrates a vulnerability in the logic flaws category.

This lab has a logic flaw in its purchasing workflow. To solve the lab, exploit this flaw to buy a &quot;Lightweight l33t leather jacket&quot;.

The vulnerability exists because the application fails to properly validate, sanitize, or secure the user-controlled input that reaches a sensitive operation. The specific attack surface and exploitation technique depend on the exact vulnerability type demonstrated in this lab.

### Recon / Initial Analysis

Based on the lab's objective and the PortSwigger solution:

1. Analyze the application's functionality to identify the attack surface
2. Log in and notice that there is a coupon code, NEWCUST5.
                    
                    
                        At the bottom of the page, sign up to the newsletter. You receive another cou
3. Use Burp Suite Proxy to intercept and analyze requests
4. Identify the specific vulnerability type by testing user-controlled input
5. Determine the appropriate exploitation technique for this lab

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

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab has a logic flaw in its purchasing workflow. To solve the lab, exploit this flaw to buy a &quot;Lightweight l33t leather jacket&quot;."

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

An attacker could purchase items at reduced prices, bypass multi-step workflows, access functionality outside their privilege level, manipulate application state for financial gain, bypass rate limits, or cause data corruption.

### Detection / Testing Methodology

1. Identify business-critical parameters (prices, quantities, discount codes, roles)
2. Test if client-side values can be modified to affect server-side logic
3. Test multi-step workflows for sequence bypass (skip steps, replay, out-of-order)
4. Check for inconsistent handling of exceptional input (very large, negative, unexpected values)
5. Test rate limits and brute-force protections
6. Look for encryption oracles and state machine flaws

### Remediation

- Implement server-side validation for all business-critical parameters (prices, quantities, roles)
- Never trust client-side values for pricing, permissions, or workflow state
- Enforce workflow sequence integrity server-side
- Use server-side state machines for multi-step processes
- Implement consistency checks for financial transactions
- Rate-limit based on business logic, not just request volume

### Key Takeaways

- This lab demonstrates a logic flaws vulnerability in a real-world scenario.
- The vulnerability occurs because user input reaches a sensitive operation without proper validation.
- The PortSwigger lab confirms: "This lab has a logic flaw in its purchasing workflow. To solve the lab, exploit this flaw to buy a &"
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Implement server-side validation for all business-critical parameters (prices, quantities, roles)
