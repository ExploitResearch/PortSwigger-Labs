# User role controlled by request parameter

### Target Goal - 

Access the admin panel and use it to delete the user `carlos`

### Analysis/Exploitation -

Browse to `/admin` and observe that you can't access the admin panel.

![](./images/31af54ec147f_001.png)

Turn on inercept and **Login as user **`wiener`**:**

Observe that the response sets the cookie `Admin=false`. Change it to `Admin=true`

![](./images/31af54ec147f_002.png)

There is a cookie called `Admin`, and it’s value is `false`**change the value to **`true`

![](./images/31af54ec147f_003.png)

Load the admin panel and delete `carlos`.

![](./images/31af54ec147f_004.png)
