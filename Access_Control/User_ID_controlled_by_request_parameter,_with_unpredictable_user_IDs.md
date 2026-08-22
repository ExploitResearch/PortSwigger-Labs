# User ID controlled by request parameter, with unpredictable user IDs

### Target Goal - 

Obtain the API key for the user `carlos` and submit it as the solution

### Analysis/Exploitation -

**Login as user **`wiener`**:**

![](./images/9f01d3203bde_001.png)

**it’s using an GUID(Globally Unique Identifier) so we can’t guess other users id**

**In the home page, we can view other people’s posts:**

![](./images/9f01d3203bde_002.png)

inspect the code and we get carlos GUID

![](./images/9f01d3203bde_003.png)

or we can Click on `carlos` and observe that the URL contains his user ID

copy it and go to my account

change your GUID with Carlos in url and we got the carlos api key

submit the carlos API key

### Why It Works

The exploit succeeds because this lab has user account page that contains the current user's existing password, prefilled in a masked input.

The official solution confirms: Log in using the supplied credentials and access the user account page. Change the &quot;id&quot; parameter in the URL to administrator. View the resp

The root cause is a failure in the application's security architecture specific to this access control scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- This lab contains current user's existing password, demonstrating how access control vulnerabilities manifest in real applications.
- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab has user account page that contains the current user's existing password, prefilled in a ma"
- Server-side authorization checks must be enforced on every request, not just the UI.

## PortSwigger Lab

**Official lab:** User ID controlled by request parameter, with unpredictable user IDs

**PortSwigger:** https://portswigger.net/web-security/access-control/lab-user-id-controlled-by-request-parameter-with-unpredictable-user-ids
