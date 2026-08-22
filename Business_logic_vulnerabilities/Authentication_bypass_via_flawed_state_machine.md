# Authentication bypass via flawed state machine

**Lab URL:** https://portswigger.net/web-security/logic-flaws/examples/lab-logic-flaws-authentication-bypass-via-flawed-state-machine

### Goal - 

Exploit logic flaw to access the admin panel and delete Carlos

### Analysis/Exploitation 

**Login as user **`wiener`**:**

What immediately jumps to attention is that the login is a two-stage process. After providing the username and the password, I can select the role I want to login as:

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Business_logic_vulnerabilities/images/fb2712cdedb1_001.png)

Such an option does make sense. It allows users with higher privileges to restrict their permissions when they don't need them. This reduces both the attack surface during everyday activities as well as the risk of stupid and expensive mistakes. At least, if done properly. Having two dedicated accounts for this is both easier and less error-prone.

I select `user` and have a look at the `/role-selector` request in Burp Proxy:

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Business_logic_vulnerabilities/images/fb2712cdedb1_002.png)

### Attempt 1: Adjust role

The second login stage contains the user role. The roles available to me are listed on the page. I don't know whether another check is done during the POST of this form.

What happens if I change the role to 'admin' or 'administrator'? Of course, I don't know the role names, but it is worth a try.

Unfortunately, this does not lead to anything, neither error nor more privileges. This indicates that on processing that POST, it validates against allowed roles and defaults to something that is not admin.

### Attempt 2: Drop request

Speaking about defaulting, what happens if the full second request is dropped? Common sense would indicate that the session is dropped if any request is made before the second stage is finished. Easy to find out.

Using Burp proxy I log in with `wiener:peter` but drop the `GET` request to `/role-selector` completely. Afterwards, then manually browse to `/my-account`. Observe that role has defaulted to the `administrator` role and have access to the admin panel.           

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Business_logic_vulnerabilities/images/fb2712cdedb1_003.png)

Now simply go to the Admin panel and use the link to delete user `carlos`.
