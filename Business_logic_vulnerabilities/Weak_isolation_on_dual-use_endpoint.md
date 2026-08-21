# Weak isolation on dual-use endpoint

### Goal - 

Exploit logic flaw to access the admin panel and delete Carlos

### Analysis/Exploitation 

**Login as user **`wiener`**:**

One thing that catches my eye is the password change functionality:

Why does it contain the username as an input field? I'd expect either the password to be changed for the logged-in user, `wiener`. In this case, the input field for the username would be unnecessary.

What happens if I use it and simply change the username to `administrator`?

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/bb5a0148-e37a-4709-9b8f-4255565d4c2e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466RVYDG32M%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215611Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCoYoDNBVf9Fo2vBR9%2FRauo%2FYDmwMU9SmDznBe1dVBWRwIgQmbiXrR0pOEIVBP7IGl9sqoZMsTTxVyNtvivvi7TePoqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDDZDXxdAJh%2BQ7JruACrcA3tKwP0wSDNdp0035Y%2FbyT%2FKlluEn1Cn4WDydIIg%2FtlwSFwlZWaSPyznsB3L5nxYVNhthEhyHDm1hgrcfS%2BmglrgbijmmSoz4QW5tLeamqM5fqWH2AI14UI62QTPOjMaA0WPebt2OemXp5XTG2BvPW7XgNuCA2I8Udum%2B7VCrKLahLwlxmuNONWsHZadiDVh2%2FPOThoWUJfk8qrgxJXUux5G7FnbR5ZH6OJI4Ru64UOo0daaJLzejJJbH68ouEnRfKY9oRaGa3dNL3V37iOmPDiIA5ZLDL7Cget6qnqLqj%2FNvyXCr6zBbNcyfpV%2Fb9WEPSH68%2BtF33Q%2F%2BWpIfT3oAodsfVZKKDiM1gQQA%2BYojJWzzfz8gW1G0uXzsV1u%2FXSwgPBGAD2%2FRSXqLZT%2Fe7AaHI95dRwsCa2DjV0eCGS%2F2zWUtFEeewBC1b0WjKZZsus2VQnGwC58%2FF4J%2BPX0bTqkweNkiBNrsM2Xg%2FUXiQled%2BXoFAavYSYSKGzLb4EM3MCUgeLCCftQ6U%2F4QAXF%2BoTIscVqns3xP5DrqSsKj3tY%2F325v1Y2G3qBfSGs5Qa%2BP2NrcypjP0CaG7Y1uKER92uGO40RfP0TVVAWNN06vFTV95epzjSxFnW5BqkmDesSMPGFo9QGOqUBNG0YiPtOTjflAfTb%2Fntqk8LEf%2F%2B4auBYUZq3OeIyl46KzTIcf6PeZv103JteyeWQPxlkwSrDgBeQf7CQyJE%2BMqPsSoFc1GXC2JK47ZgoBRHg1gQHibhdpe6HRqt3FBr7Zr3Alq5yaU6yXepYMLbxnXvOufOHtD8YSbsbS2l1B9FxF00%2B%2F8WUFszFczEFDE4DMMWSU6z%2BFA8XgS0%2B5W7bxxMl0IqQ&X-Amz-Signature=78ba1532cd133875daa1b4ab809be085962a384c26b878cf5991b4da73f11f4f&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

We get error Current password is incorrect:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e6e26397-57bd-4650-a628-543c7609a0a8/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466WUDMN5L5%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215612Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIENzhKaL49114aE3QtLJ6nr1pxuYEU5MmRfIRt63CfOOAiEAuSQbsUVtFUcnAFeAxydzkUbmQ43%2Fx5lm%2BHLu%2BIzKkVUqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDKjaqrOx6H2LBYRIjCrcA5IKKyaXF0CdmFH5WHjzXcmum1oATElOS70BIGC3DAgv1SCiDoOBqFc8x3BIvpr%2BKWtyqdW%2By%2FB1x25sL911%2FM8aR5jp7CXKpscvMitTbJWCphJA0N4mvJucW6%2BmrhCrQVNuW6fdtHSJ%2Ftkb8sS2zrd8EuDUf9kaj7Yy45qi3w882gZPyFiGVFTgQ%2FV7D2CV17EJd5U%2BQL9AENbKxw8F75I7ScoO8LL46axggaBGIbigrizcgBoIdC4hEAtqHioj2gfWwikQ%2FP91hAV4RUO5suk40%2BmpR%2BD07%2F5N6dXYbg507JsRCC2yd3IWsW8bG%2FDiagAQURqZuwEGKNczV9zvJ0VnCDlImKRopOeQBpMwIGc%2BcpnhGJoL9F8smbScaI7U1zcqiOAdw6OWYgIQw2IUoQfHwbCICRNCFlhnfN3PQAUiCU3x5xKHlBq1kVY00AgFzSHk7O9G7HS4j0VnycZbWYa6OcpvUXW7%2BFKVFIZwzyKwo%2FN3QAwjhMvFYg%2Bh5DtEcJz%2FqfKcwznpsHUc7RRUSus4FA%2BWlc5YLJhUxWQa18Lay8crwTeOuG%2F10Q3Mevj9flQIn5NFjvvSDUSlCDg8g8FQ0Z%2FAT8jBCwKOvm57au79VoqGvCvXvlzQ41pLMPKDo9QGOqUBGz%2FmdqTqG3Ass3GNKhzHgXXEiXvaCkvaEshptXqIDAJurIiR%2F6T%2BZkarkwMIDc7gIAvw2miYPaBVDua5eEZIUlhnCmWlh5sJuFwiAHBQj4Qe2jQwAsWHC78bIZ5fpjeKTbQyevbT5NE7QOGgl1msFfjZvIvzn72c00i%2BJpztXySvQ5WpATQcDyIjlSiLRUb2n3LPg%2FT9bPy0gppXmqbemTbNW729&X-Amz-Signature=d3d17b146d49cc504aead274f995dcc4586f7a755f657f3c8c49d58f970df39c&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

From this result I can derive a few pieces of information:

1. The password change failed due to a wrong current password.
1. The password comparison was not performed with the password account that is logged in but with the password of the account set in `Username`
1. At the point the 'Update password' form was generated, the application did use the logged-in user again.

But at some point during the generation of the response, the application assumed that my username is `administrator`. This points to some weird logic behind the scenes that warrant further investigation.

To verify that no password was changed despite the error message, I attempt to log in with both `wiener` and `administrator` using the newly set password. It fails as expected.

### Analyzing the traffic

When we clicked the `Change password` button, **it send a POST request to **`/my-account/change-password`**, with parameter **`csrf`**, **`username`**, **`current-password`**, **`new-password-1`**, and **`new-password-2`**.**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/81e66630-f649-477b-94d3-afd5f40c0120/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466RVYDG32M%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215611Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCoYoDNBVf9Fo2vBR9%2FRauo%2FYDmwMU9SmDznBe1dVBWRwIgQmbiXrR0pOEIVBP7IGl9sqoZMsTTxVyNtvivvi7TePoqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDDZDXxdAJh%2BQ7JruACrcA3tKwP0wSDNdp0035Y%2FbyT%2FKlluEn1Cn4WDydIIg%2FtlwSFwlZWaSPyznsB3L5nxYVNhthEhyHDm1hgrcfS%2BmglrgbijmmSoz4QW5tLeamqM5fqWH2AI14UI62QTPOjMaA0WPebt2OemXp5XTG2BvPW7XgNuCA2I8Udum%2B7VCrKLahLwlxmuNONWsHZadiDVh2%2FPOThoWUJfk8qrgxJXUux5G7FnbR5ZH6OJI4Ru64UOo0daaJLzejJJbH68ouEnRfKY9oRaGa3dNL3V37iOmPDiIA5ZLDL7Cget6qnqLqj%2FNvyXCr6zBbNcyfpV%2Fb9WEPSH68%2BtF33Q%2F%2BWpIfT3oAodsfVZKKDiM1gQQA%2BYojJWzzfz8gW1G0uXzsV1u%2FXSwgPBGAD2%2FRSXqLZT%2Fe7AaHI95dRwsCa2DjV0eCGS%2F2zWUtFEeewBC1b0WjKZZsus2VQnGwC58%2FF4J%2BPX0bTqkweNkiBNrsM2Xg%2FUXiQled%2BXoFAavYSYSKGzLb4EM3MCUgeLCCftQ6U%2F4QAXF%2BoTIscVqns3xP5DrqSsKj3tY%2F325v1Y2G3qBfSGs5Qa%2BP2NrcypjP0CaG7Y1uKER92uGO40RfP0TVVAWNN06vFTV95epzjSxFnW5BqkmDesSMPGFo9QGOqUBNG0YiPtOTjflAfTb%2Fntqk8LEf%2F%2B4auBYUZq3OeIyl46KzTIcf6PeZv103JteyeWQPxlkwSrDgBeQf7CQyJE%2BMqPsSoFc1GXC2JK47ZgoBRHg1gQHibhdpe6HRqt3FBr7Zr3Alq5yaU6yXepYMLbxnXvOufOHtD8YSbsbS2l1B9FxF00%2B%2F8WUFszFczEFDE4DMMWSU6z%2BFA8XgS0%2B5W7bxxMl0IqQ&X-Amz-Signature=1cf33f2e880669af917d4f2be25bd83b59a325a4849a29c3fc3825c2bcb7732b&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

OK, so I have the csrf token, username and the three password parameters.

While the application generated the response, at the moment my username was embedded, I was the `administrator` user. I was also considered `administrator` while the current password was checked and the error message got inserted. As such, the password change failed as it was not the correct password for that user.

So what happens if I remove the current-password parameter from the form?

This depends on whether it always checks the current password on password change. If this is the case, then it will fail as well, as it should.

However, if the password check only occurs when the parameter is present, then it will be bad for the application but good for me.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/2fc35871-6a2d-4cb6-92f8-1016672f0b1d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466RVYDG32M%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215611Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCoYoDNBVf9Fo2vBR9%2FRauo%2FYDmwMU9SmDznBe1dVBWRwIgQmbiXrR0pOEIVBP7IGl9sqoZMsTTxVyNtvivvi7TePoqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDDZDXxdAJh%2BQ7JruACrcA3tKwP0wSDNdp0035Y%2FbyT%2FKlluEn1Cn4WDydIIg%2FtlwSFwlZWaSPyznsB3L5nxYVNhthEhyHDm1hgrcfS%2BmglrgbijmmSoz4QW5tLeamqM5fqWH2AI14UI62QTPOjMaA0WPebt2OemXp5XTG2BvPW7XgNuCA2I8Udum%2B7VCrKLahLwlxmuNONWsHZadiDVh2%2FPOThoWUJfk8qrgxJXUux5G7FnbR5ZH6OJI4Ru64UOo0daaJLzejJJbH68ouEnRfKY9oRaGa3dNL3V37iOmPDiIA5ZLDL7Cget6qnqLqj%2FNvyXCr6zBbNcyfpV%2Fb9WEPSH68%2BtF33Q%2F%2BWpIfT3oAodsfVZKKDiM1gQQA%2BYojJWzzfz8gW1G0uXzsV1u%2FXSwgPBGAD2%2FRSXqLZT%2Fe7AaHI95dRwsCa2DjV0eCGS%2F2zWUtFEeewBC1b0WjKZZsus2VQnGwC58%2FF4J%2BPX0bTqkweNkiBNrsM2Xg%2FUXiQled%2BXoFAavYSYSKGzLb4EM3MCUgeLCCftQ6U%2F4QAXF%2BoTIscVqns3xP5DrqSsKj3tY%2F325v1Y2G3qBfSGs5Qa%2BP2NrcypjP0CaG7Y1uKER92uGO40RfP0TVVAWNN06vFTV95epzjSxFnW5BqkmDesSMPGFo9QGOqUBNG0YiPtOTjflAfTb%2Fntqk8LEf%2F%2B4auBYUZq3OeIyl46KzTIcf6PeZv103JteyeWQPxlkwSrDgBeQf7CQyJE%2BMqPsSoFc1GXC2JK47ZgoBRHg1gQHibhdpe6HRqt3FBr7Zr3Alq5yaU6yXepYMLbxnXvOufOHtD8YSbsbS2l1B9FxF00%2B%2F8WUFszFczEFDE4DMMWSU6z%2BFA8XgS0%2B5W7bxxMl0IqQ&X-Amz-Signature=a6ceca8078ec3a797534026d9b0bfdff16b54c84b0511e8063a373106a6d9b8a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

We successfully changed `administrator`’s password!

Try to logout and login again, this time with the credentials `administrator:peter`:

And I appear to be inside the administrator account. The application states that my username is `administrator` and it provides me with a link to an `Admin panel`. I access it, delete `carlos` and receive a confirmation:
