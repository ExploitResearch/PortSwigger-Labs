# URL-based access control can be circumvented

**Lab URL:** https://portswigger.net/web-security/access-control/lab-url-based-access-control-can-be-circumvented

### Target Goal - 

Access the admin panel and delete the user `carlos`.

### Analysis/Exploitation -

there are navbar contents consisting of Home, Admin Panel, and My Account.When trying to access the Admin Panel, the web display the text “access denied”.

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Access_Control/images/de1f871fd5cb_001.png)

Let’s try to intercept when we want to access the admin panel using the burp suite. Here’s how it looks.

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Access_Control/images/de1f871fd5cb_002.png)

Based on the intercept results, the HTTP request method “Get” points to the /admin directory.

Let’s try to use non-standard HTTP headers that can replace the URL in the original request such as X-Original-URL to bypass admin access.

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Access_Control/images/de1f871fd5cb_003.png)

It still doesn’t work :(

According to the lab description, “the front-end system has been configured to block external access to that path”. Let’s try to remove “admin” in the HTTP request method “get” so that it only leaves “/”.

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Access_Control/images/de1f871fd5cb_004.png)

The response displays 200 OK, which means the admin access was successfully bypassed. Next, find out how to delete the user Carlos to complete this lab.

Search “delete” or scroll down a bit in the response. We will find the path “/admin/delete” with the query string “?username=carlos” which leads to the user data deletion function with the parameter “username” which is “Carlos”.

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Access_Control/images/de1f871fd5cb_005.png)

Let’s try adding it to the X-Original-Url and run it.

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Access_Control/images/de1f871fd5cb_006.png)

The response will show “HTTP/2 400 Bad Request” with the message “Missing parameter ‘username’”. This indicates that the server did not read the query string “?username=carlos” in the X-Original-Url. So for the query string, we can try moving it to Get /?username=carlos.

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Access_Control/images/de1f871fd5cb_007.png)

The response displays 302 Found with the directory location /admin, which means the URL function has successfully deleted the user with the username Carlos.

If we check back to the /admin directory, the Carlos user no longer exists.

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Access_Control/images/de1f871fd5cb_008.png)

### Why It Works

To solve the lab, access the admin panel and delete the user carlos.

### Key Takeaways

- To solve the lab, access the admin panel and delete the user carlos.
