# Weak isolation on dual-use endpoint

**Lab URL:** https://portswigger.net/web-security/logic-flaws/examples/lab-logic-flaws-weak-isolation-on-dual-use-endpoint

### Goal - 

Exploit logic flaw to access the admin panel and delete Carlos

### Analysis/Exploitation 

**Login as user **`wiener`**:**

One thing that catches my eye is the password change functionality:

Why does it contain the username as an input field? I'd expect either the password to be changed for the logged-in user, `wiener`. In this case, the input field for the username would be unnecessary.

What happens if I use it and simply change the username to `administrator`?

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Business_logic_vulnerabilities/images/11e553804bdf_001.png)

We get error Current password is incorrect:

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Business_logic_vulnerabilities/images/11e553804bdf_002.png)

From this result I can derive a few pieces of information:

1. The password change failed due to a wrong current password.
1. The password comparison was not performed with the password account that is logged in but with the password of the account set in `Username`
1. At the point the 'Update password' form was generated, the application did use the logged-in user again.

But at some point during the generation of the response, the application assumed that my username is `administrator`. This points to some weird logic behind the scenes that warrant further investigation.

To verify that no password was changed despite the error message, I attempt to log in with both `wiener` and `administrator` using the newly set password. It fails as expected.

### Analyzing the traffic

When we clicked the `Change password` button, **it send a POST request to **`/my-account/change-password`**, with parameter **`csrf`**, **`username`**, **`current-password`**, **`new-password-1`**, and **`new-password-2`**.**

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Business_logic_vulnerabilities/images/11e553804bdf_003.png)

OK, so I have the csrf token, username and the three password parameters.

While the application generated the response, at the moment my username was embedded, I was the `administrator` user. I was also considered `administrator` while the current password was checked and the error message got inserted. As such, the password change failed as it was not the correct password for that user.

So what happens if I remove the current-password parameter from the form?

This depends on whether it always checks the current password on password change. If this is the case, then it will fail as well, as it should.

However, if the password check only occurs when the parameter is present, then it will be bad for the application but good for me.

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Business_logic_vulnerabilities/images/11e553804bdf_004.png)

We successfully changed `administrator`’s password!

Try to logout and login again, this time with the credentials `administrator:peter`:

And I appear to be inside the administrator account. The application states that my username is `administrator` and it provides me with a link to an `Admin panel`. I access it, delete `carlos` and receive a confirmation:
