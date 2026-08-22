# Multi-step process with no access control on one step

**Lab URL:** https://portswigger.net/web-security/access-control/lab-multi-step-process-with-no-access-control-on-one-step

### Target Goal - 

Log in using the credentials `wiener:peter` and exploit the flawed access controls to promote yourself to become an administrator

### Analysis/Exploitation -

**Let’s login as **`administrator`

**Browse to the admin panel, promote **`carlos`

When administrator try to upgrade a user, it’ll send a POST request to `/admin-roles`, with parameter: `username` and `action` (`upgrade`/`downgrade`).

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Access_Control/images/9479c2d43281_001.png)

After sending a POST request, a confirm page will be prompt, If we click `Yes`, it’ll send a POST request again:

However, this time we see 1 more parameter: `confirmed` is set to `true`.

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Access_Control/images/9479c2d43281_002.png)

**send the both steps POST request to Burp Repeater.**

With above information, we can login as user `wiener`, and try to escalate our privilege to administrator:

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Access_Control/images/9479c2d43281_003.png)

copy wiener’s session id 

Change the session id and username to wiener in both steps post request which we send to repeater

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Access_Control/images/9479c2d43281_004.png)

in first step we get unauthorized

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Access_Control/images/9479c2d43281_005.png)

**But the back-end doesn’t check the second step in upgrading a user’s privilege**

Response displays 302 Found with directory location /admin, which means the URL function has successfully upgraded the user with username wiener to admin.

refresh the page to see we’re an administrator or not

The admin panel shows that the wiener account has been promoted to admin.
