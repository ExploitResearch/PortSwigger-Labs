# Unprotected admin functionality with unpredictable URL

**Lab URL:** https://portswigger.net/web-security/access-control/lab-unprotected-admin-functionality-with-unpredictable-url

### Target Goal - 

access the admin panel, and using it to delete the user `carlos`

### Analysis/Exploitation -

**On inspecting source code it is found that contains some JavaScript that discloses the URL of the admin panel.**

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Access_Control/images/360b2846da1f_001.png)

Go to admin panel and delete carlos

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Access_Control/images/360b2846da1f_002.png)

### Why It Works

This lab has an unprotected admin panel.

### Key Takeaways

- This lab has an unprotected admin panel.
