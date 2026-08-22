# Infinite money logic flaw

### Goal - 

Exploit logic flaw to buy a “Lightweight l33t leather jacket”

### Analysis/Exploitation 

**Login as user **`wiener`**:**

The shop itself looks very familiar, but my account page has a new feature - I can use gift cards. Additionally, the lab provides access to my emails.

![](./images/74167a3dd6e5_001.png)

The gift cards can be purchased for $10.

![](./images/74167a3dd6e5_002.png)

To find out how this works, simply buy one:

![](./images/74167a3dd6e5_003.png)

We get gift card code at bottom and At the same time, I received an email, also containing the gift card code:

![](./images/74167a3dd6e5_004.png)

On the 'My account' website I can apply the gift card to bring my store credit back up to $100. Unfortunately, I can not apply the gift card a second time. 

The gift card code can also not be used as a coupon on the checkout page.

Nothing obviously fishy comes up upon checking the requests in Burp.

### Subscribing to newsletter

There is newsletter subscription at the bottom of the home page, we can sign up to their newsletter.

![](./images/74167a3dd6e5_005.png)

Subscribe to find out if there is any interesting reward for it:

![](./images/74167a3dd6e5_006.png)

It is a 30% discount. This makes me think... The gift card states $10 flat rate value, can I apply the 30% on this? (after all, all shops I know in real life exclude gift cards explicitly from discounts)

![](./images/74167a3dd6e5_007.png)

So for $7 I can purchase a $10 gift card that redeems for face value.

After the code is generated and applied to my account, the store credit total shows $3 higher than before:

![](./images/74167a3dd6e5_008.png)

### Purchasing gift cards

For the $98 store credit, I can purchase 14 gift cards, generating a $3 profit each and a total of $42

![](./images/74167a3dd6e5_009.png)

To obtain the $1337 required to purchase the leather jacket, I need to redeem more than 400 gift cards. This is nothing I want to do manually, even though it could be a little less (<300) if I apply the 30% coupon for the jacket itself as well.

### Create a macro

In settings go to "Project" > "Sessions". In the "Session handling rules" panel, click "Add". The "Session handling rule editor" dialog opens. In the dialog, go to the "Scope" tab. Under "URL Scope", select "Include all URLs".  

![](./images/74167a3dd6e5_010.png)

Go back to the "Details" tab. Under "Rule actions", click "Add" > "Run a macro". Under "Select macro", click "Add" again to open the Macro Recorder. 

The first thing is selecting the proper requests for a macro.

![](./images/74167a3dd6e5_011.png)

Then, click "OK". The Macro Editor opens. 

In the list of requests, select `GET /cart/order-confirmation?order-confirmed=true`. Click "Configure item". In the dialog that opens, click "Add" to create a custom parameter. Name the parameter `gift-card` and highlight the gift card code at the bottom of the response. Click "OK" twice to go back to the Macro Editor.

![](./images/74167a3dd6e5_012.png)

Select the `POST /gift-card` request and click "Configure item" again. In the "Parameter handling" section, use the drop-down menus to specify that the `gift-card` parameter should be derived from the prior response (response 4). Click "OK".                   

![](./images/74167a3dd6e5_013.png)

In the Macro Editor, click "Test macro". Look at the response to `GET /cart/order-confirmation?order-confirmation=true` and note the gift card code that was generated. Look at the `POST /gift-card` request. Make sure that the `gift-card` parameter matches and confirm that it received a `302` response. Keep clicking "OK" until you get back to the main Burp window.

### Automate it

Now the macro test is successful, the parameter is obtained automatically and the gift card is applied. So I create a session rule that runs this macro for every request:

Send the `GET /my-account` request to Burp Intruder and use:

- Attack type: **Sniper**
- Payload: Null payloads, continue indefinitely
- Resource Pool: 1 concurrent request
the requests must be made in order, so I use a resource pool with "Maximum concurrent requests" set to `1`.

While the attack is running, refreshing of the account page in the browser shows a steady increase in store credit. So let it run for a while...

After around 400 request the credit score get enough to buy the jacket then stop intruder

Now place the order

### Why It Works

The exploit succeeds because this lab has a logic flaw in its purchasing workflow. to solve the lab, exploit this flaw to buy a &quot;lightweight l33t leather jacket&quot;.

The official solution confirms: This solution uses Burp Intruder to automate the process of buying and redeeming gift cards. Users proficient in Python might prefer to use the Turbo 

The root cause is a failure in the application's security architecture specific to this logic flaws scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab has a logic flaw in its purchasing workflow. To solve the lab, exploit this flaw to buy a &"
- Validate business-critical parameters server-side — never trust client-supplied values.

## PortSwigger Lab

**Official lab:** Infinite money logic flaw

**PortSwigger:** https://portswigger.net/web-security/logic-flaws/examples/lab-logic-flaws-infinite-money
