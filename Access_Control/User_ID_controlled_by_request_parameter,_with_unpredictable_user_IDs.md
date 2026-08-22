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
