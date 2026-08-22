# Low-level logic flaw

### Goal - 

Exploit logic flaw to buy the Lightweight l33t leather jacket.


### Vulnerability / Concept

This lab demonstrates a web security vulnerability that can be exploited to compromise the application's security. The vulnerability allows an attacker to bypass security controls and perform unauthorized actions.

The core issue is a failure in the application's security architecture — either insufficient input validation, broken access controls, improper trust boundaries, or insecure handling of user-supplied data. Understanding the root cause is essential for both exploitation and remediation.

### Recon / Initial Analysis

1. Identify the attack surface — what user-controlled inputs exist (URL parameters, form fields, headers, cookies)
2. Analyze the application's behavior with unexpected input
3. Map the request flow and identify trust boundaries
4. Test for error messages that reveal implementation details
5. Compare authenticated vs unauthenticated behavior
6. Use Burp Suite Proxy to capture and analyze all requests
7. Check for hidden parameters using Burp Intruder or Param Miner

### Analysis/Exploitation 

**Login as user **`wiener`**:**

Let’s try to buy the leather jacket!

When we clicked the `Add to cart` button, **it’ll send a POST request to **`/cart`**, with parameter **`productId=1`**, **`redir=PRODUCT`** and **`quantity=1`**.**

![](./images/5ad590f44e73_001.png)

send them to repeater to use them later

On sending the `quantity` to a negative value? Like `-2`, It doesn’t add negative quantity of products. So it dont’t work

![](./images/5ad590f44e73_002.png)

We neither can’t add more than 99 quantiy

![](./images/5ad590f44e73_003.png)

In the `Add to cart` button’s HTML form, we can see that the `quantity` has a limit, the minimum number is `0`, and the maximum is `99`.

![](./images/5ad590f44e73_004.png)

**Note:**The maximum number of items that can be added to the cart is 99 and it is a limit on adding product in single time not on max quantity we can buy, So we can add as many product as we want but max-99 in each request.

{% hint style="info" %}
💡 Another thing worth trying is attempting to create an overflow with the price. The price is stored in some type of numeric variable. Once it exceeds the maximum value, it usually overflows to the lowest possible value and continues to count up from there:

|  |  |
|---|---|
| **current value** | **new value after calculating +1** |
| 1 | 2 |
| 2 | 3 |
| max_value | min_value |
| min_value | min_value + 1 |

Of course, the exact values for `min_value` and `max_value` depend on the data types used and could range into very, very high numbers.

{% endhint %}


**Now, what if the total price is greater than a maximum value of an integer?** (Integer overflow)

![](./images/5ad590f44e73_005.png)

**If the total price is greater than **`2147483647`**, will the price went to **`0`**?**

Send the add to cart request which is **POST request to **`/cart` into intruder

In Burp Intruder, set the quantity of the request to 99, add a Null payload and continue indefinitely. To be able to observe the website, I also only allow a single concurrent request in the resource 
pool.

- Attack type: **Sniper**
- Payload: Null payloads, continue indefinitely
- Resource Pool: 1 concurrent request

![](./images/5ad590f44e73_006.png)

After a couple of refreshes while Burp Intruder sends its request, the page shows a negative number: 

Try to order when total price is negative but Unfortunately, it is prevented by the application:

![](./images/5ad590f44e73_007.png)

{% hint style="info" %}
💡 The price has exceeded the maximum value permitted for an integer in the back-end programming language (2,147,483,647). As a result, the value has looped back around to the minimum possible value (-2,147,483,648) and starts counting up towards 0 then turn positive again.

**when the total price reached greater than **`2147483647`**, the value will become negative, then it’ll go back to positive again!**

{% endhint %}


### **Adjusting the total value**

Note that the price of the jacket is stored in cents (133700). 

![](./images/5ad590f44e73_008.png)

so after around 162 requests of 99 quantity each, the price will turn into negative and after sending another 162 request price will comes near to 0.

Adding 32123 jackets brings the price to $-1221

![](./images/5ad590f44e73_009.png)

Adding another 1 jacket increases total to $115 which is above our store credit

So find some other product to bring the total price in the range between zero and $100.

![](./images/5ad590f44e73_010.png)

My total cart value negative $1221 So add (1221/69.61=17.54) 18 quantiy of potato theater

![](./images/5ad590f44e73_011.png)

Now Place order

### Why It Works

The vulnerability exists because the application fails to properly validate, sanitize, or authorize user input. The broken trust boundary allows an attacker to manipulate the application's behavior by injecting unexpected data that the server processes without adequate security checks.

### Real-World Impact

An attacker could exploit this vulnerability to:
- Access sensitive data belonging to other users
- Bypass authentication or authorization controls
- Perform unauthorized actions on behalf of legitimate users
- Potentially achieve remote code execution on the server
- Compromise the integrity or availability of the application

### Remediation

- Implement proper server-side input validation for all user-controlled data
- Use parameterized queries and prepared statements
- Enforce server-side authorization checks on every request
- Follow the principle of least privilege
- Implement security headers (CSP, X-Frame-Options, X-Content-Type-Options)
- Use a Web Application Firewall (WAF) as defense-in-depth
- Regularly test for vulnerabilities using automated scanners and manual testing

### Key Takeaways

- Never trust user-controlled input — validate and sanitize everything server-side.
- Security controls must be enforced server-side, not client-side.
- Understanding the vulnerability's root cause is essential for proper remediation.
- Burp Suite is essential for identifying and exploiting web vulnerabilities.
- Defense in depth — use multiple layers of protection, not just one.
