# Inconsistent security controls

### Goal - 

Exploit logic flaw to access the admin panel and delete Carlos



### Vulnerability / Concept

This lab demonstrates a vulnerability in the logic flaws category.

This lab's flawed logic allows arbitrary users to access administrative functionality that should only be available to company employees. To solve the lab, access the admin panel and delete the user carlos.

The vulnerability exists because the application fails to properly validate, sanitize, or secure the user-controlled input that reaches a sensitive operation. The specific attack surface and exploitation technique depend on the exact vulnerability type demonstrated in this lab.

### Recon / Initial Analysis

Based on the lab's objective and the PortSwigger solution:

1. Analyze the application's functionality to identify the attack surface
2. Open the lab then go to the &quot;Target&quot; &gt; &quot;Site map&quot; tab in Burp. Right-click on the lab domain and select &quot;Engagement tools&quot; &gt; &quot;Discover content&quot; to open th
3. Use Burp Suite Proxy to intercept and analyze requests
4. Identify the specific vulnerability type by testing user-controlled input
5. Determine the appropriate exploitation technique for this lab

### Analysis/Exploitation 

I can register a new account and see that employees of DontWannaCry should use their company email. As I do not have one I register a new account with my email address from the email client:

![](./images/b14b568648ba_001.png)

Once I register, I receive an email with a confirmation link to complete the registration In my email client.

![](./images/b14b568648ba_002.png)

After confirming the email, I can log into my account.

On doing site-mapping/content-dicovery , discovered the path `/admin`.

**the admin panel is in **`/admin`**,But it’s only available to DontWannaCry user.**

![](./images/b14b568648ba_003.png)

On the `my account` page, there is update email option. What happens if I simply change it to a `@dontwannacry.com` one? 

![](./images/b14b568648ba_004.png)

After clicking on the `Update email` button, two things become obvious:

1. My email address is changed straight away
1. An `Admin panel` link appeared

![](./images/b14b568648ba_005.png)

This shows two things:

1. There is no validation on changing the email
1. The existence of an `@dontwannacry.com` email entry is the sole condition for access to the admin panel

So now go to admin panel and **Let’s delete user **`carlos`**:**

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab's flawed logic allows arbitrary users to access administrative functionality that should only be available to company employees. To solve the lab, access the admin panel and delete the user c"

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
- The PortSwigger lab confirms: "This lab's flawed logic allows arbitrary users to access administrative functionality that should on"
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Implement server-side validation for all business-critical parameters (prices, quantities, roles)
