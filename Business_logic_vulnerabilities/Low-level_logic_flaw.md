# Low-level logic flaw

**Lab URL:** https://portswigger.net/web-security/logic-flaws/examples/lab-logic-flaws-low-level

### Goal - 

Exploit logic flaw to buy the Lightweight l33t leather jacket.

### Analysis/Exploitation 

**Login as user **`wiener`**:**

Let’s try to buy the leather jacket!

When we clicked the `Add to cart` button, **it’ll send a POST request to **`/cart`**, with parameter **`productId=1`**, **`redir=PRODUCT`** and **`quantity=1`**.**

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Business_logic_vulnerabilities/images/5ad590f44e73_001.png)

send them to repeater to use them later

On sending the `quantity` to a negative value? Like `-2`, It doesn’t add negative quantity of products. So it dont’t work

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Business_logic_vulnerabilities/images/5ad590f44e73_002.png)

We neither can’t add more than 99 quantiy

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Business_logic_vulnerabilities/images/5ad590f44e73_003.png)

In the `Add to cart` button’s HTML form, we can see that the `quantity` has a limit, the minimum number is `0`, and the maximum is `99`.

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Business_logic_vulnerabilities/images/5ad590f44e73_004.png)

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

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Business_logic_vulnerabilities/images/5ad590f44e73_005.png)

**If the total price is greater than **`2147483647`**, will the price went to **`0`**?**

Send the add to cart request which is **POST request to **`/cart` into intruder

In Burp Intruder, set the quantity of the request to 99, add a Null payload and continue indefinitely. To be able to observe the website, I also only allow a single concurrent request in the resource 
pool.

- Attack type: **Sniper**
- Payload: Null payloads, continue indefinitely
- Resource Pool: 1 concurrent request

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Business_logic_vulnerabilities/images/5ad590f44e73_006.png)

After a couple of refreshes while Burp Intruder sends its request, the page shows a negative number: 

Try to order when total price is negative but Unfortunately, it is prevented by the application:

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Business_logic_vulnerabilities/images/5ad590f44e73_007.png)

{% hint style="info" %}
💡 The price has exceeded the maximum value permitted for an integer in the back-end programming language (2,147,483,647). As a result, the value has looped back around to the minimum possible value (-2,147,483,648) and starts counting up towards 0 then turn positive again.

**when the total price reached greater than **`2147483647`**, the value will become negative, then it’ll go back to positive again!**

{% endhint %}

### **Adjusting the total value**

Note that the price of the jacket is stored in cents (133700). 

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Business_logic_vulnerabilities/images/5ad590f44e73_008.png)

so after around 162 requests of 99 quantity each, the price will turn into negative and after sending another 162 request price will comes near to 0.

Adding 32123 jackets brings the price to $-1221

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Business_logic_vulnerabilities/images/5ad590f44e73_009.png)

Adding another 1 jacket increases total to $115 which is above our store credit

So find some other product to bring the total price in the range between zero and $100.

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Business_logic_vulnerabilities/images/5ad590f44e73_010.png)

My total cart value negative $1221 So add (1221/69.61=17.54) 18 quantiy of potato theater

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Business_logic_vulnerabilities/images/5ad590f44e73_011.png)

Now Place order
