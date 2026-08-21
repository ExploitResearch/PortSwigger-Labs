# Username enumeration via account lock

[Username enumeration via account lock](https://portswigger.net/web-security/authentication/password-based/lab-username-enumeration-via-account-lock)

I try to login with an (allegedly) invalid username and see if it locks me out based on my IP.

For this, I use the null payload option to generate 50 login attempts. But even after the 50th request, it still states ‘Invalid username or password’ and does not mention any lockout.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/36d45cae-e5cf-47df-a70d-026cf58754ce/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466ZZWXLGC6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204537Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCgr%2BFRxG5SDbSRbVLU09M%2BI9cCmUaayuUuqlrpvonCjwIhAP%2FJEUrE0BjBgVyuh9kezeMLxKgyM4q0u1E3ZeCaPnEcKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgySKA2%2F9JgU4IPWMg4q3ANC8t34PLq9qNcBGzPvRooqKp1IfXUSDppDC2tWFa459v8Vx9jYUiUy6IvzwmTCseQ9ywqSTF6gEwriW4vMNlktuvljzcGFHa6FRF1Ho%2BZLmZa6QTpBIS%2BgperOAG1H7x9tlDbKSlHUr05GNwiqXxGnHkjyxvw5MhrS7nzUBe%2Bz8DhhIImZkizzDe3Owt22%2FeAP8nJscK31VAo7eqPCbMoGqs26v8L%2Bd82nFFx5utjNUvU3sWGBhPViyu9N6ZfNi2do3l4dyS0HbLZ83CCM%2B45Lz2f3QhDOvToADqt72nDg5FrsrFCzVddum5sf0f9e1SSjJCrI7AOXIg%2FXqeWYIoHlXhQ2oOt1SwnURrYtcnH0YvGXhXvigjzTuTEL2rQskCZYFEcOLDhUDmc6k2irwRMNQ6razA798PbeU%2F87NNXmlWbXjFDlFqjvDuIaZbNNObM6ZfiUIUNCsivoS7V%2FERXG%2FBMtZwoDF0WU2t%2BuWRIhwZrIFDnyayDd2T68F%2BVGobgGGnDmSt0j8Oguzm%2BKhuikwfmT4eakRG99dqjr%2F9flDHj%2FIBHRGuMjW%2FvlK7WR85sSXOvvIvNyyecFO4F801mPg7stHpcyMJzlIapGqvyKmpGaG4TRerAzaFi4wDDGyqLUBjqkAcJkgtkcZ%2BEPt5KyfYTq%2BHMzBkNC9T%2B1tADKSCB9DBeJp%2Bb95bNzv4m%2FeIVAX%2Bzl0%2ByQMgUvZwMSMl2j83DRDpHMC1KZdY3UDEqZRnn8xoJ4YQhJvDNFiSXe084%2FyWx8M6ghGN1fDppEw9NEAca%2BxU6%2Byf5J4Eo05BBUiZOo7Z1e6DvwTzK5sv9kzzLFAuh%2BxBDjY4YZcJWw0jtypeQEoPLh7jD6&X-Amz-Signature=61ff16703f54b7b969c735a77591afd864d3f8cb30fb0603b412780db47ce01e&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

That means it does not trigger based on login attempts from one source, but on existing accounts only. So I repeat the last step, this time making multiple requests for each possible username and see whether there is a different behavior or message.

- With Burp running, investigate the login page and submit an invalid username and password. Send the `POST /login` request to Burp Intruder.
- Select the attack type **Cluster bomb**. Add a payload position to the `username` parameter. Add a blank payload position to the end of the request body by clicking **Add §** twice. The result should look something like this: `username=§invalid-username§&password=example§§`
- On the **Payloads** tab, add the list of usernames to the first payload set. For the second set, select the **Null payloads** type and choose the option to generate 5 payloads. This will
effectively cause each username to be repeated 5 times. Start the attack.
- In the results, notice that the responses for one of the usernames were longer than responses when using other usernames. Study the response more closely and notice that it contains a different error message: `You have made too many incorrect login attempts.` Make a note of this username.
- Create a new Burp Intruder attack on the `POST /login` request, but this time select the **Sniper** attack type. Set the `username` parameter to the username that you just identified and add a payload position to the `password` parameter.
- Add the list of passwords to the payload set and create a grep extraction rule for the error message. Start the attack.
- In the results, look at the grep extract column. Notice that there are a couple of different error messages, but one of the responses did not contain any error message. Make a note of this
password.
- Wait for a minute to allow the account lock to reset. Log in using the username and password that you identified and access the user account page to solve the lab.
