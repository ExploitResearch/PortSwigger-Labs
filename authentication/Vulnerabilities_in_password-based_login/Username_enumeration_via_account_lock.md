# Username enumeration via account lock

[Username enumeration via account lock](https://portswigger.net/web-security/authentication/password-based/lab-username-enumeration-via-account-lock)

I try to login with an (allegedly) invalid username and see if it locks me out based on my IP.

For this, I use the null payload option to generate 50 login attempts. But even after the 50th request, it still states ‘Invalid username or password’ and does not mention any lockout.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/36d45cae-e5cf-47df-a70d-026cf58754ce/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4667LDQ3JE6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221718Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQD13TAcnK933YtCVFGfV%2BwOUMKxrxNqy4hNm4boryArsgIgQCPvXpAcit2ibX5tKzHMbUn6E8wyqLyOVPrelNHukRsqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDCWdeE2BeuXiQ38WGircA7qp0%2Fplct1YWqkGrhvYvtcauvMT7RW1nxgGSVaWJJi%2FZrUsk%2Fz3cWpCcwWazp5xxXgmcnHdmXHMmYkZDmT9zSHPfp8GNGnXScVpFL%2FVewjGmSuy1Dq3fYhmcAjxdk0kZFUWxK4UERwqXY9aNK7L5BHEVWF8jkwTSMw8TLQEc4R62ezFfKfJC4ZGpB2h7D1ViB4n1YcjQNFFtDUJTvShvLdpeGZCrD6ZwsxvDx2F4W0mbM3%2BAKssCFiU66lsCfRkpQkftsSx0lucyoDG%2BSnc6Z%2FOzdFKgYkwDT9oNlpAY8d8g4aM%2Bv8P%2BfjcAyHmvZbCmd7%2BC6zl3ZVEb0S1hna3rcQ%2FQ02VnyJHOmP4aIFlcAHhiPTMWmlDofJ7Us6wKEm7g%2BO2bnI8GEBrm%2FRA4Q1TpZnB%2BajUz0tDIOYRk0nBOl8DmFRyO3jZo9Bp0vLiraumfna%2BaIHP4E%2FzIiappv7JOy6RXLBNIOU8j2RB0WnH0SwhmSXfH3B3z01pQjn1tWo3ZHb4tRQlEqlnw7%2BwzIVLok3zUWPiaQGgTuui%2B1L8XC3ES7sn1npdDVyFMGtzL16rKBKJ5EyILz5FGZR8d9NqbrvZg3FAbhnrMz0Q8vYtGc2VVT2tFMzxF8MFV2m9MOaFo9QGOqUBbU37CV%2BH5LkZ78zvGUs%2FeoQaxvtrGSxZUoG3h38N%2BJ1UE5Vi7ac9nCF0Gq9jhv2aoU%2BCMZ3HbbVXQ4fyPoOLHevDQiJBZyZTXQ6AL9ZM2xn7oWmw79fBeouNvWT289DrN%2BesMOMNb26iIP%2BJAUY72l0rsoIx380MLsT056PFAjkXYQidADrbFHAyqz5UW2%2BBORbnklH9%2FctVLK0AuiDSmQGhy3XF&X-Amz-Signature=bbf439e727388e4e14962e526acc2413b448145cea1bc50750b32713a256d158&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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
