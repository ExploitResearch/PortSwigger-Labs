# Basic password reset poisoning

- Go to the login page and notice the "Forgot your password?" functionality. Request a password reset for your own account.
- Go to the exploit server and open the email client. Observe that you have received an email containing a link to reset your password. Notice that the URL contains the query parameter `temp-forgot-password-token`.
- Click the link and observe that you are prompted to enter a new password. Reset your password to whatever you want.
- In Burp, study the HTTP history. Notice that the `POST /forgot-password` request is used to trigger the password reset email. This contains the username whose password is being reset as a body parameter. Send this request to Burp Repeater.
- In Burp Repeater, observe that you can change the Host header to an arbitrary value and still successfully trigger a password reset. Go back to the email server and look at the new email
that you've received. Notice that the URL in the email contains your arbitrary Host header instead of the usual domain name.
- Back in Burp Repeater, change the Host header to your exploit server's domain name (`YOUR-EXPLOIT-SERVER-ID.exploit-server.net`) and change the `username` parameter to `carlos`. Send the request.
![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/HTTP_Host_Header_Attacks/images/30f4987cb066_001.png)

- Go to your exploit server and open the access log. You will see a request for `GET /forgot-password` with the `temp-forgot-password-token` parameter containing Carlos's password reset token. Make a note of this token.
- Go to your email client and copy the genuine password reset URL from your first email. Visit this URL in the browser, but replace your reset token with the one you obtained from the access log.
- Change Carlos's password to whatever you want, then log in as `carlos` to solve the lab.

### Why It Works

The exploit succeeds because this lab is vulnerable to password reset poisoning. the user carlos will carelessly click on any links in emails that he receives. to solve the lab, log in to carlos's account.

The official solution confirms: Go to the login page and notice the &quot;Forgot your password?&quot; functionality. Request a password reset for your own account. Go to the exploit 

The root cause is a failure in the application's security architecture specific to this host header scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab is vulnerable to password reset poisoning. The user carlos will carelessly click on any lin"
- Validate the Host header against an allowlist of expected domains.

## PortSwigger Lab

**Official lab:** Basic password reset poisoning

**PortSwigger:** https://portswigger.net/web-security/host-header/exploiting/password-reset-poisoning/lab-host-header-basic-password-reset-poisoning
