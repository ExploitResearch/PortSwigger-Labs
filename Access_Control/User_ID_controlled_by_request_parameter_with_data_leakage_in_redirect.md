# User ID controlled by request parameter with data leakage in redirect

**Lab URL:** https://portswigger.net/web-security/access-control/lab-user-id-controlled-by-request-parameter-with-data-leakage-in-redirect

### Target Goal - 

Obtain the API key for the user `carlos` and submit it as the solution

### Analysis/Exploitation -

**Login as user **`wiener`**:**

- Send the request to Burp Repeater.
- Change the "id" parameter to `carlos`.
- Observe that although the response is now
redirecting you to the home page, it has a body containing the API key
belonging to `carlos`.

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Access_Control/images/e4ef3ed98f03_001.png)

Submit the API key.
