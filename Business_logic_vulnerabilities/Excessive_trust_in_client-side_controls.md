# Excessive trust in client-side controls

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

**Login as user **`wiener`**:**

Attempt to buy the leather jacket. We only have `$100` store credit**,** The order get rejected because of not having enough store credit.

![](./images/fa1b4a7f9625_001.png)

**analyze the request in burp proxy that have been sent so far**

Trying to modify the price on the cart page is not useful, as this information has already been sent from the server and we are not affecting any back-end information.

We also don’t have control over how much store credit we have. The only interaction that we were able to make happen, prior to the cart page, is the “add product to cart” step.

The request to add product to the cart looks rather promising, as it contains the price as a parameter.If  cannot find this request, go to browser and re-add the item to cart.

Remove any existing cart items. Then, go to Burp Suite’s `Proxy > HTTP history` page and find the add-product request. This is a `POST` request to `/cart`.

![](./images/fa1b4a7f9625_002.png)

When we clicked add to cart button, **it send a POST request to **`/cart`** with parameter: **`productId=1`**, **`redir=PRODUCT`**, **`quantity=1`**, and **`price=133700`**.**

We’re transmitting price information from the client to the server. This is the “excessive trust”. We, as a client, are telling the server how much the product costs.

Now if the input is not sanitized by the server. An attacker can change the quantity of the product or change the price.

Modify the price value to something less than the $100.00 that we have in store credit: notice there are two more zeros in price parameter so **set the price to 100 i.e.($1.00)**

![](./images/fa1b4a7f9625_003.png)

Now go back to your browser, and in cart section click `Place Order`.

![](./images/fa1b4a7f9625_004.png)

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
