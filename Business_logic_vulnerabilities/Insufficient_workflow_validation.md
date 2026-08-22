# Insufficient workflow validation

### Goal - 

Exploit logic flaw to buy a “Lightweight l33t leather jacket”

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
