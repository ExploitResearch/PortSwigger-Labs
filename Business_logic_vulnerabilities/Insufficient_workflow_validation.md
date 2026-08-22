# Insufficient workflow validation

### Goal - 

Exploit logic flaw to buy a “Lightweight l33t leather jacket”



### Vulnerability / Concept

This lab demonstrates a vulnerability in the logic flaws category.

This lab makes flawed assumptions about the sequence of events in the purchasing workflow. To solve the lab, exploit this flaw to buy a &quot;Lightweight l33t leather jacket&quot;.

The vulnerability exists because the application fails to properly validate, sanitize, or secure the user-controlled input that reaches a sensitive operation. The specific attack surface and exploitation technique depend on the exact vulnerability type demonstrated in this lab.

### Recon / Initial Analysis

Based on the lab's objective and the PortSwigger solution:

1. Analyze the application's functionality to identify the attack surface
2. With Burp running, log in and buy any item that you can afford with your store credit.
                    
                    
                        Study the proxy history. Observe that when you 
3. Use Burp Suite Proxy to intercept and analyze requests
4. Identify the specific vulnerability type by testing user-controlled input
5. Determine the appropriate exploitation technique for this lab

### Analysis/Exploitation 

**Login as user **`wiener`**:**

From the description this lab uses the already well known web shop application again. First to have a quick look around for new features, than I login to my account. As usual, I have a $100 store credit and need to purchase an article for much more than that.

When trying to purchase it, I get an expected `Not enough store credit for this purchase` error. Looking into the requests in Burp, I notice something odd though:

![](./images/aea74cfcd9d7_001.png)

The checkout generates a `303 See Other` response, which instructs my browser to follow up with a GET to the indicated page. The interesting part here is, that the location includes a logical workflow status - the fact that I have not enough funds. I wonder what happens if I purchase something that I can afford:

![](./images/aea74cfcd9d7_002.png)

Here, the redirect goes to another page with an order confirmation.When we have enough store credits, **it’ll send a GET request to **`/cart/order-confirmation`**, with parameter **`order-confirmed=true`**.**

Let's try to purchase the jacket again, but intercept the calls and change the redirect destination.** send a GET request to **`/cart/order-confirmation`** with parameter **`order-confirmed=true`

![](./images/aea74cfcd9d7_003.png)

After all the requests went through, the lab shows success

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab makes flawed assumptions about the sequence of events in the purchasing workflow. To solve the lab, exploit this flaw to buy a &quot;Lightweight l33t leather jacket&quot;."

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
- The PortSwigger lab confirms: "This lab makes flawed assumptions about the sequence of events in the purchasing workflow. To solve "
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Implement server-side validation for all business-critical parameters (prices, quantities, roles)
