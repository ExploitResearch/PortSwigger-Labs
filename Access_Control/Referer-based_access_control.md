# Referer-based access control

**Lab URL:** https://portswigger.net/web-security/access-control/lab-referer-based-access-control

### Target Goal - 

Log in using the credentials `wiener:peter` and exploit the flawed access controls to promote yourself to become an administrator

### Analysis/Exploitation -

**Let’s login as **`administrator`

**Browse to the admin panel and promote **`carlos`

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Access_Control/images/9f5bc07a9e8d_001.png)

When an administrator try to upgrade a user, it send a GET request to `/admin-roles`, with the parameter: `username` and `action` (`upgrade`/`downgrade`).

Also, it includes a `Referer` HTTP header!

**login as user **`wiener`**, and try to escalate privilege to administrator:**

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Access_Control/images/9f5bc07a9e8d_002.png)

send it to repeater and change GET request to `/admin-roles`, with the parameter: `username=wiener&action=upgrade` 

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Access_Control/images/9f5bc07a9e8d_003.png)

we get `Unauthorized` error.

In the above GET request, we can see that it includes a `Referer` HTTP header , change that to `/admin` Which is the admin panel location

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Access_Control/images/9f5bc07a9e8d_004.png)

**Let’s refresh the page and we’re administrator now**
