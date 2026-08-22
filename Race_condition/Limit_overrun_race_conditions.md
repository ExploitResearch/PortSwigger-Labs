# Limit overrun race conditions        

### Goal - 

 Purchase a **Lightweight L33t Leather Jacket**.



### Vulnerability / Concept

This lab demonstrates a vulnerability in the race conditions category.

This lab's purchasing flow contains a race condition that enables you to purchase items for an unintended price.

The vulnerability exists because the application fails to properly validate, sanitize, or secure the user-controlled input that reaches a sensitive operation. The specific attack surface and exploitation technique depend on the exact vulnerability type demonstrated in this lab.

### Recon / Initial Analysis

1. Analyze the application's functionality and identify user-controlled inputs
2. Use Burp Suite to intercept and modify requests
3. Test for the specific race conditions vulnerability
4. Identify the injection point and context
5. Craft an appropriate payload

### Analysis/Exploitation -

![](./images/e7e7c62b1122_001.png)

In home page, we can see that the promotion code `PROMO20` for 20% off, and we can purchase some items.

**Login as user** `wiener`**:**

Now, let's try to purchase the "Lightweight L33t Leather Jacket":

**Apply the coupon code** `PROMO20`**:**

![](./images/e7e7c62b1122_002.png)

When we clicked the "Apply" button, it'll send a POST request to `/cart/coupon`, with parameter `csrf` and `coupon`.

We still do not have enough store credit for this purchase after applying coupon.

![](./images/e7e7c62b1122_003.png)

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

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab's purchasing flow contains a race condition that enables you to purchase items for an unintended price."

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
- The PortSwigger lab confirms: "This lab's purchasing flow contains a race condition that enables you to purchase items for an unint"
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Implement proper database transactions with appropriate isolation levels
