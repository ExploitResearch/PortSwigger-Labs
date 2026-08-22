# Username enumeration via subtly different responses

**Lab URL:** https://portswigger.net/web-security/authentication/password-based/lab-username-enumeration-via-subtly-different-responses

1. With Burp running, submit an invalid username and password. Send the `POST /login` request to Burp Intruder and add a payload position to the `username` parameter.
					
2. On the **Payloads** tab, make sure that the **Simple list** payload type is selected and add the list of candidate usernames.
					
3. On the **Settings** tab, under **Grep - Extract**, click **Add**. In the dialog that appears, scroll down through the response until you find the error message `Invalid username or password.`. Use the mouse to highlight the text content of the message. The other settings will be automatically adjusted. Click **OK** and then start the attack.
					
4. When the attack is finished, notice that there is an additional column containing the error message you extracted. Sort the results using this column to notice that one of them is subtly different.

5. Look closer at this response and notice that it contains a typo in the error message - instead of a full stop/period, there is a trailing space. Make a note of this username.

6. Close the attack and go back to the **Positions** tab. Insert the username you just identified and add a payload position to the `password` parameter:
`username=identified-user&password=§invalid-password§`

7. On the **Payloads** tab, clear the list of usernames and replace it with the list of passwords. Start the attack.	

8. When the attack is finished, notice that one of the requests received a `302` response. Make a note of this password.

9. Log in using the username and password that you identified and access the user account page to solve the lab.
						**
Note**
It's also possible to brute-force the login using a single cluster bomb attack. However, it's generally much more efficient to enumerate a valid username first if possible.

adsl

killer
