# Excessive trust in client-side controls

**Lab URL:** https://portswigger.net/web-security/logic-flaws/examples/lab-logic-flaws-excessive-trust-in-client-side-controls

### Goal - 

Exploit logic flaw to buy the Lightweight l33t leather jacket.

### Analysis/Exploitation 

**Login as user **`wiener`**:**

Attempt to buy the leather jacket. We only have `$100` store credit**,** The order get rejected because of not having enough store credit.

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Business_logic_vulnerabilities/images/fa1b4a7f9625_001.png)

**analyze the request in burp proxy that have been sent so far**

Trying to modify the price on the cart page is not useful, as this information has already been sent from the server and we are not affecting any back-end information.

We also don’t have control over how much store credit we have. The only interaction that we were able to make happen, prior to the cart page, is the “add product to cart” step.

The request to add product to the cart looks rather promising, as it contains the price as a parameter.If  cannot find this request, go to browser and re-add the item to cart.

Remove any existing cart items. Then, go to Burp Suite’s `Proxy > HTTP history` page and find the add-product request. This is a `POST` request to `/cart`.

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Business_logic_vulnerabilities/images/fa1b4a7f9625_002.png)

When we clicked add to cart button, **it send a POST request to **`/cart`** with parameter: **`productId=1`**, **`redir=PRODUCT`**, **`quantity=1`**, and **`price=133700`**.**

We’re transmitting price information from the client to the server. This is the “excessive trust”. We, as a client, are telling the server how much the product costs.

Now if the input is not sanitized by the server. An attacker can change the quantity of the product or change the price.

Modify the price value to something less than the $100.00 that we have in store credit: notice there are two more zeros in price parameter so **set the price to 100 i.e.($1.00)**

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Business_logic_vulnerabilities/images/fa1b4a7f9625_003.png)

Now go back to your browser, and in cart section click `Place Order`.

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Business_logic_vulnerabilities/images/fa1b4a7f9625_004.png)

### Why It Works

This lab doesn't adequately validate user input.

### Key Takeaways

- This lab doesn't adequately validate user input.
