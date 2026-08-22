# Password reset broken logic

- With Burp running, click the **Forgot your password?** link and enter your own username.
- Click the **Email client** button
to view the password reset email that was sent. Click the link in the
email and reset your password to whatever you want.
- In Burp, go to **Proxy > HTTP history** and study the requests and responses for the password reset
functionality. Observe that the reset token is provided as a URL query
parameter in the reset email. Notice that when you submit your new
password, the `POST /forgot-password?temp-forgot-password-token` request contains the username as hidden input. Send this request to Burp Repeater.
- In Burp Repeater, observe that the password
reset functionality still works even if you delete the value of the `temp-forgot-password-token` parameter in both the URL and request body. This confirms that the token is not being checked when you submit the new password.
- In the browser, request a new password reset and change your password again. Send the `POST /forgot-password?temp-forgot-password-token` request to Burp Repeater again.
- In Burp Repeater, delete the value of the `temp-forgot-password-token` parameter in both the URL and request body. Change the `username` parameter to `carlos`. Set the new password to whatever you want and send the request.
- In the browser, log in to Carlos's account using the new password you just set. Click **My account** to solve the lab.

### Why It Works

The exploit succeeds because this lab's password reset functionality is vulnerable. to solve the lab, reset carlos's password then log in and access his &quot;my account&quot; page.

The official solution confirms: With Burp running, click the Forgot your password? link and enter your own username. Click the Email client button to view the password reset email th

The root cause is a failure in the application's security architecture specific to this authentication scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab's password reset functionality is vulnerable. To solve the lab, reset Carlos's password the"
- Consistent error messages and rate-limiting prevent enumeration and brute-force.
