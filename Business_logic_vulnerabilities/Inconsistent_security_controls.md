# Inconsistent security controls

**Lab URL:** https://portswigger.net/web-security/logic-flaws/examples/lab-logic-flaws-inconsistent-security-controls

### Goal - 

Exploit logic flaw to access the admin panel and delete Carlos

### Analysis/Exploitation 

I can register a new account and see that employees of DontWannaCry should use their company email. As I do not have one I register a new account with my email address from the email client:

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Business_logic_vulnerabilities/images/b14b568648ba_001.png)

Once I register, I receive an email with a confirmation link to complete the registration In my email client.

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Business_logic_vulnerabilities/images/b14b568648ba_002.png)

After confirming the email, I can log into my account.

On doing site-mapping/content-dicovery , discovered the path `/admin`.

**the admin panel is in **`/admin`**,But it’s only available to DontWannaCry user.**

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Business_logic_vulnerabilities/images/b14b568648ba_003.png)

On the `my account` page, there is update email option. What happens if I simply change it to a `@dontwannacry.com` one? 

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Business_logic_vulnerabilities/images/b14b568648ba_004.png)

After clicking on the `Update email` button, two things become obvious:

1. My email address is changed straight away
1. An `Admin panel` link appeared

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/Business_logic_vulnerabilities/images/b14b568648ba_005.png)

This shows two things:

1. There is no validation on changing the email
1. The existence of an `@dontwannacry.com` email entry is the sole condition for access to the admin panel

So now go to admin panel and **Let’s delete user **`carlos`**:**
