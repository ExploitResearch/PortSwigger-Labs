# Method-based access control can be circumvented

**Lab URL:** https://portswigger.net/web-security/access-control/lab-method-based-access-control-can-be-circumvented

### Target Goal - 

Log in using the credentials `wiener:peter` and exploit the flawed access controls to promote yourself to become an administrator

### Analysis/Exploitation -

<details><summary>Summary</summary>

We can see this request with administrator user.

```text
POST /admin-roles HTTP/1.1
...
username=carlos&action=upgrade

```

```text

POST /admin-roles - HTTP/1.1   -->401 Unauthorized
GET /admin - HTTP/1.1   -->400 Missing parameter'username'
```

With non privileged user, we  get 401 Unauthorized error.

But we can bypass the error with another type of request instead of using POST.

```text
GET /admin-roles?username=wiener&action=upgrade HTTP/1.1 --> 302 Found
GET /admin --> 200 OK
```

</details>

familiarize yourself with the admin panel by logging in using the credentials `administrator:admin` 

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Access_Control/images/730f8a45256c_001.png)

Here, administrator can upgrade or downgrade a user.

When we try to upgrade a user:

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Access_Control/images/730f8a45256c_002.png)

**It’s sending a POST request to **`/admin-roles`**, and with the **`username`** and **`action`**.**

Now, let’s log out and login as user `wiener` to do vertical privilege escalation!

After login send any GET request to repeater and change the ** **location to** **`/admin-roles`

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Access_Control/images/730f8a45256c_003.png)

As you can see, looks like we can access `/admin-roles` when we’re sending a GET request to `/admin-roles` without any parameters.

If we change it to POST method we  get 401 Unauthorized . **So we’re allowed to send a GET request to **`/admin-roles`

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Access_Control/images/730f8a45256c_004.png)

**send a GET request to **`/admin-roles`**, with parameters: **`username=wiener&action=upgrade`**:**

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Access_Control/images/730f8a45256c_005.png)
