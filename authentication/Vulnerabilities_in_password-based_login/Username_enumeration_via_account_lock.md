# Username enumeration via account lock

[Username enumeration via account lock](https://portswigger.net/web-security/authentication/password-based/lab-username-enumeration-via-account-lock)

I try to login with an (allegedly) invalid username and see if it locks me out based on my IP.

For this, I use the null payload option to generate 50 login attempts. But even after the 50th request, it still states ‘Invalid username or password’ and does not mention any lockout.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/36d45cae-e5cf-47df-a70d-026cf58754ce/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4663WQDBP4G%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215346Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIHx%2FDIWu%2BsuWqmyOaz6nbQb9uegm1uYi0hE2a0KxGfZuAiBXtDi1uP8JYAvg0mFpJ2BGEdW0m6Nm3aoyGk2jeDeyoSqIBAiu%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMl0zcL2O4Vq8GLYYVKtwDX8hzkCeS9ygx8DhtcOfi4X%2BRdMC6YPxDAbUqIyhSCkJ2CkgoTYZRbCIwv33IGVnbChCFiWCbE9X8WygzcowNHWuGtd2ujJhvDyFTUWhbJnNXZZuyXSS9EgSRXWnmn3XZRnO0JMZWpZRUmjrDl7dua3xPh68%2Fkb9Il2hemjgjtUIp3wN11pVyOxv6VpT3gr3mOOs%2BdSS7uTbp4LTRTcx3%2BFtM4F%2BWrAfVytxFV0kUm06vT1yrQpWcYmzhz0DCcRVyuRqCoqMsiJEoz2K9e4ioUufC8G1V4nq3M93HV9%2FQBghmXGayjC%2BACMOdx%2B%2F9UrzqTZeXn84YqXDKpKqfRZ91sJPPQ%2BY0J%2F3sh1ML5RTbXGe7iT%2BO1xbpAGqWGke%2BN56SPnsiEgsfLOIRewDeEV2GaZHHdMzmkBc4yOeRPgEWgAaq0tQYaNOCatVzNfhPLY1tAzqZkQZPDxwBFa2GHOGB1GrFB1FfvAQcG6vtrOfcUuJt65ehJxmMdH1lBO8NrJH0fZmeY74lKbUJ29cn7S3CN7D2ILbR5DccRvACm6YHGt2HIELtvab0xCGSFILdTeG14ypwgqCyHSGzBeUjUd%2Fmyr0%2Fn5i0AfbacsdHGh%2BoT65QVzzRN%2F%2FDGzEKH34wh4Sj1AY6pgHoQ7cKqAqn1nqGlJ%2BugdG%2BII70%2Bpq321ypVqiOmbj80nmFaKnKe3YZGp9xmOVs2deMfl9RpK76RyS%2BCHMGOGhujy61k%2BIzZmj4su1u2WQvDJO0lzLkqw1jir8BDmiJ%2B521UAaX2%2FUUbSDEjqQod7%2F5SAgcvlS2mF3HFrLKugnnx9P37e1MUQncWDppWDhX6YsU%2BWyGmuoi5vCbp46BkoZtWbMFiC%2Fm&X-Amz-Signature=89867cdfa6d209209310da844ac32c91be02219ddde8d6d2c999bc943acac15c&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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
