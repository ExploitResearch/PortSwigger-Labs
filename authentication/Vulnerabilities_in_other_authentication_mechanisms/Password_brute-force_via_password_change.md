# Password brute-force via password change

- With Burp running, log in and experiment with the password change functionality. Observe that the username is submitted as hidden input in the request.
- Notice the behavior when you enter the wrong current password. If the two entries for the new password match, the account is locked. However, if you enter two different new passwords, an error message simply states `Current password is incorrect`. If you enter a valid current password, but two different new passwords, the message says `New passwords do not match`. We can use this message to enumerate correct passwords.
- Enter your correct current password and two new passwords that do not match. Send this `POST /my-account/change-password` request to Burp Intruder.
- In Burp Intruder, change the `username` parameter to `carlos` and add a payload position to the `current-password` parameter. Make sure that the new password parameters are set to two different values. For example: `username=carlos&current-password=§incorrect-password§&new-password-1=123&new-password-2=abc`
- On the **Payloads** tab, enter the list of passwords as the payload set
- On the **Settings** tab, add a grep match rule to flag responses containing `New passwords do not match`. Start the attack.
- When the attack finished, notice that one response was found that contains the `New passwords do not match` message. Make a note of this password.
- In the browser, log out of your own account and lock back in with the username `carlos` and the password that you just identified.

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/authentication/Vulnerabilities_in_other_authentication_mechanisms/images/4c716c36435f_001.png)

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/authentication/Vulnerabilities_in_other_authentication_mechanisms/images/4c716c36435f_002.png)

- Click **My account** to solve the lab.

### Why It Works

The exploit succeeds because this lab's password change functionality makes it vulnerable to brute-force attacks. to solve the lab, use the list of candidate passwords to brute-force carlos's account and access his &quot;my accou

The official solution confirms: With Burp running, log in and experiment with the password change functionality. Observe that the username is submitted as hidden input in the request

The root cause is a failure in the application's security architecture specific to this authentication scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab's password change functionality makes it vulnerable to brute-force attacks. To solve the la"
- Consistent error messages and rate-limiting prevent enumeration and brute-force.

## PortSwigger Lab

**Official lab:** Password brute-force via password change

**PortSwigger:** https://portswigger.net/web-security/authentication/other-mechanisms/lab-password-brute-force-via-password-change
