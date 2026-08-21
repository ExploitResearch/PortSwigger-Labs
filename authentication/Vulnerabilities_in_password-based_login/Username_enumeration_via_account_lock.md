# Username enumeration via account lock

[Username enumeration via account lock](https://portswigger.net/web-security/authentication/password-based/lab-username-enumeration-via-account-lock)

I try to login with an (allegedly) invalid username and see if it locks me out based on my IP.

For this, I use the null payload option to generate 50 login attempts. But even after the 50th request, it still states ‘Invalid username or password’ and does not mention any lockout.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/36d45cae-e5cf-47df-a70d-026cf58754ce/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4664WHE6FR5%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210222Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCx4T1tKFXrV1B6pzbm5341r9aK8afv%2F4JQcITcAhlGoAIhANFRrDt5ySjSr49c%2F4fQb%2F6mQUBBdQgw25Dund59VwBGKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgxNdxTdi9W0JlIhDPIq3APjl0QEUSXK1hzO6PxuCkILo6M%2FCkMy4Pe1PNI1HxAHzu1vJHvbhtd1peqRUKv5%2BBePAan2gsyQMw5ol6r830%2F9%2BmsSaveZOVI8LPdYX7IHFe%2FK2o8DMi9aHiQG51FtkMO%2FLD%2BBkaUED%2Fo5ktqzBqiJBHA%2F7WxkIYlnFESgeisAAxUMmCalBppFu%2FMucBgwvaZsTPTXusRdKA3YB64S6L%2BUl%2B%2BvWS4RuyHiEm%2F6QlRHXj3PKocXFJWRN0Ocg3uBlKUo4SmaZHyuSus99Bb0fvCYFi85FMOBwe4mZsaeyJluTDNTqi28uPM6JB%2FVDZVil94SqUZDbeDjVZbuscaz9QtqwRn2AA8n1lt3YyV6x2HP0jPxp1eVNQf7s7XuouXqQlDzCeZodjEbHwTP0oRq6ddPRfy48eiW5o1bv59WKD5bJ5L6q3RPEMqLAPY9D%2Fas%2FmaMwFxgOWr4FqaqYPonHhaxZ58ZieUf7fMem39SChVXxzlXLE9cWAwaVUUqoqGsSmT7jqTBIelb4jqYRD2ylKO6%2FnkHg6%2B5j93b8yGENXQVZ3ErdywybtQXP4XpxxxzFYb6txd%2Fkpbixymy0WREPm6m6JmOSyN%2FXN8MHftEkkiTX3gVVenWtG83LiUBMDC5xqLUBjqkAZ6QhGf%2BUgZ5%2FLKTa3t9YOKaop9eRFbUXOApI6V%2BZyoHL3mQQp2wDarMP3DR8rbmvYu4LE8Aqf%2FMVUxkO%2Ft6HHhtx7A54L9upugUhBa8GywEkd2Aqm0tbLQY5HcAipHlXh2b3HfmG7bGEGlkFN4yaE7uXknpM4NHCEdZKsi%2BqS2R%2F9suiwUAMahPVU7Padv3BvJHU6%2Fbl%2FGaMEWMwkneHEsWOY7R&X-Amz-Signature=39c3119ec90283d3513ebab36650ca0522af4b06c61d0a6c06aa829e33c50956&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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
