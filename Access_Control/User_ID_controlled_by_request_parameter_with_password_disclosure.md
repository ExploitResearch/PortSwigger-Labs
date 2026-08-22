# User ID controlled by request parameter with password disclosure

### Target Goal - 

Retrieve the administrator’s password, then use it to delete `carlos`.

### Analysis/Exploitation -

**Login as user **`wiener`**:**

password is** prefilled in a masked input** and we can see by inspecting code

![](./images/d1f96ac1c92a_001.png)

we can see that our password is reflecting in response

![](./images/d1f96ac1c92a_002.png)

Change the "id" parameter to `administrator`.

![](./images/d1f96ac1c92a_003.png)

![](./images/d1f96ac1c92a_004.png)

**View the response in Burp and observe that it contains the administrator's password**

**login as **`administrator`** and delete user **`carlos`**!**

## PortSwigger Lab

**Official lab:** User ID controlled by request parameter with password disclosure

**PortSwigger:** https://portswigger.net/web-security/access-control/lab-user-id-controlled-by-request-parameter-with-password-disclosure
