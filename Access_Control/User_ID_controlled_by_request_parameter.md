# User ID controlled by request parameter

### Target Goal - 

Obtain the API key for the user `carlos` and submit it as the solution

### Analysis/Exploitation -

**Login as user **`wiener`**:**

Change id=carlos in url

{% hint style="info" %}
💡 This is an example of an insecure direct object reference (IDOR) 
vulnerability. This type of vulnerability arises where user-controller 
parameter values are used to access resources or functions directly.
{% endhint %}

![](./images/0a874cee4a12_001.png)

Submit the Carlos API key
