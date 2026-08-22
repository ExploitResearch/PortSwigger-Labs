# Inconsistent security controls

### Goal - 

Exploit logic flaw to access the admin panel and delete Carlos

### Analysis/Exploitation 

I can register a new account and see that employees of DontWannaCry should use their company email. As I do not have one I register a new account with my email address from the email client:

![](./images/b14b568648ba_001.png)

Once I register, I receive an email with a confirmation link to complete the registration In my email client.

![](./images/b14b568648ba_002.png)

After confirming the email, I can log into my account.

On doing site-mapping/content-dicovery , discovered the path `/admin`.

**the admin panel is in **`/admin`**,But it’s only available to DontWannaCry user.**

![](./images/b14b568648ba_003.png)

On the `my account` page, there is update email option. What happens if I simply change it to a `@dontwannacry.com` one? 

![](./images/b14b568648ba_004.png)

After clicking on the `Update email` button, two things become obvious:

1. My email address is changed straight away
1. An `Admin panel` link appeared

![](./images/b14b568648ba_005.png)

This shows two things:

1. There is no validation on changing the email
1. The existence of an `@dontwannacry.com` email entry is the sole condition for access to the admin panel

So now go to admin panel and **Let’s delete user **`carlos`**:**

### Why It Works

The exploit succeeds because this lab's flawed logic allows arbitrary users to access administrative functionality that should only be available to company employees. to solve the lab, access the admin panel and delete the user c

The official solution confirms: Open the lab then go to the &quot;Target&quot; &gt; &quot;Site map&quot; tab in Burp. Right-click on the lab domain and select &quot;Engagement tools&

The root cause is a failure in the application's security architecture specific to this logic flaws scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab's flawed logic allows arbitrary users to access administrative functionality that should on"
- Validate business-critical parameters server-side — never trust client-supplied values.

## PortSwigger Lab

**Official lab:** Inconsistent security controls

**PortSwigger:** https://portswigger.net/web-security/logic-flaws/examples/lab-logic-flaws-inconsistent-security-controls
