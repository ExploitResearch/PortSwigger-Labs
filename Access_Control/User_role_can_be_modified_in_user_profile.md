# User role can be modified in user profile

### Target Goal - 

Access the admin panel and use it to delete the user `carlos`

### Analysis/Exploitation -

**Login as user **`wiener`**:**

**In here, we can **`Update email`**. Let’s intercept that POST request /my-account/change-email and sent it to Repeater!**

![](./images/d967f51a9a7f_001.png)

**set the **`roleid`** to 2 in request, Which is  user **`administrator`** as in lab description **

![](./images/d967f51a9a7f_002.png)

**go to the admin panel (**`/admin`**) and **delete user `carlos`!
