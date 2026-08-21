# SameSite Strict bypass via client-side redirect

### Goal - 

use your exploit server to host an HTML page that uses a CSRF attack to change the viewer’s email address.

### Analysis/Exploitation -

Login as user `wiener`:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e634db50-9ad5-48ed-8357-fe079046d56f/2024-02-22_19-57.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UENM3UAL%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215459Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIGNW%2B6XlS8gqFirtnnLUVTdXXNi8PnvxiW1h4FdlbyO8AiBqb986u3Na4DpecKU1rydMx8u2lmgJzQYie%2BjPwAlcfCqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMXYFA15qNoYL4wMRjKtwD%2F2Nxqvbvqq6ZAeWHMddzDTSTw%2Fw3N8PxJRYizMqOLKLT5CutQ%2B6NNHu87qfeqsAmYwIGN%2FrSSYQ9yt7jrF0bJErOXmW%2B1aliQtCei9sbK%2FfSA%2Fv0spEyDtq9jVFm8R3HV8kbQlx1ayvOGFF40ULF%2F8yGV%2BsmpQyHgU9NdLr%2FDL2d14NuNJfg3G4xYIWdLi3uWmfI%2BdX%2FP%2BPH8ujPyBO%2FvBG9XHUxsZeB6iEHyu4h7Z2XSa85MBD%2FAF%2FuFUErV8AsHk1zSwiINGnWuL%2FeWCNls14jKYZILXTzQci7OIXEyUesYfOotlR6iOctKWXZfaiX50Zrwp7CevCTwGo9rYSIr2oL%2BS6UEUsg61gvgoLYlrcFI05GfmzKaE9PserMdi5t%2BsYFx7MMm1N2%2FSaHnOeDtCb1tQWbTvpCAIVdXeR%2FcBaB%2FQB0NwA4aGdJ9TxvmXfBfzOFdD1umkHj4zdLaHPBN8xMpZp1i6DBjtsTCaqhf6IeiX%2FYeJX5MrsVzTE9O9ZcFJ22XOcjBW12ZtjuTbUAoVJV7ky82VKHFgMuiQtGcvz9yO9bzdSIg%2FT6txtCG3sLMuNwCha9P9PY3%2BUXe8oH1v7LfBIpcmOyycIChH6DM46M7DHrOtXV3RlPSz0wmIaj1AY6pgHn4h2Lg5%2FiaVBLun9yfn3fpDmmswj6xCIckQtZaOpqjnANvahR3TpP9kSGnF7%2FvyUbsnV3447TxNH%2FXPdUIFEeYR6QlGqGbzPv9v9KK2BuhV3oSHDPtGWI%2F4sWlxGkiur1jUnOcKlfjuhgZAtubu0DTDxijlCVpnkvGAhV6Gg%2FySqdsUvotse75qjT7y9lwmlfFOtMCRXIzJyXAYzcBymRBI0Hq4WD&X-Amz-Signature=d899fb9e23a9a731ad5ab21ff0a1e3dac3dfc7a9f38ee79361fe1d3499761108&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

it’ll set a new session cookie for us: we can see there is a `SameSite` attribute, which is set to `Strict` restriction.

**Inspect the change-email request **

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/bb6cd652-6676-475b-8f9a-32fed3dd743a/2024-02-22_20-05.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UENM3UAL%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215459Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIGNW%2B6XlS8gqFirtnnLUVTdXXNi8PnvxiW1h4FdlbyO8AiBqb986u3Na4DpecKU1rydMx8u2lmgJzQYie%2BjPwAlcfCqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMXYFA15qNoYL4wMRjKtwD%2F2Nxqvbvqq6ZAeWHMddzDTSTw%2Fw3N8PxJRYizMqOLKLT5CutQ%2B6NNHu87qfeqsAmYwIGN%2FrSSYQ9yt7jrF0bJErOXmW%2B1aliQtCei9sbK%2FfSA%2Fv0spEyDtq9jVFm8R3HV8kbQlx1ayvOGFF40ULF%2F8yGV%2BsmpQyHgU9NdLr%2FDL2d14NuNJfg3G4xYIWdLi3uWmfI%2BdX%2FP%2BPH8ujPyBO%2FvBG9XHUxsZeB6iEHyu4h7Z2XSa85MBD%2FAF%2FuFUErV8AsHk1zSwiINGnWuL%2FeWCNls14jKYZILXTzQci7OIXEyUesYfOotlR6iOctKWXZfaiX50Zrwp7CevCTwGo9rYSIr2oL%2BS6UEUsg61gvgoLYlrcFI05GfmzKaE9PserMdi5t%2BsYFx7MMm1N2%2FSaHnOeDtCb1tQWbTvpCAIVdXeR%2FcBaB%2FQB0NwA4aGdJ9TxvmXfBfzOFdD1umkHj4zdLaHPBN8xMpZp1i6DBjtsTCaqhf6IeiX%2FYeJX5MrsVzTE9O9ZcFJ22XOcjBW12ZtjuTbUAoVJV7ky82VKHFgMuiQtGcvz9yO9bzdSIg%2FT6txtCG3sLMuNwCha9P9PY3%2BUXe8oH1v7LfBIpcmOyycIChH6DM46M7DHrOtXV3RlPSz0wmIaj1AY6pgHn4h2Lg5%2FiaVBLun9yfn3fpDmmswj6xCIckQtZaOpqjnANvahR3TpP9kSGnF7%2FvyUbsnV3447TxNH%2FXPdUIFEeYR6QlGqGbzPv9v9KK2BuhV3oSHDPtGWI%2F4sWlxGkiur1jUnOcKlfjuhgZAtubu0DTDxijlCVpnkvGAhV6Gg%2FySqdsUvotse75qjT7y9lwmlfFOtMCRXIzJyXAYzcBymRBI0Hq4WD&X-Amz-Signature=70f6de6710a6559857ba6c5081c663207be26d8ea9546095ec81ed3286b8fdee&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

It doesn’t have a CSRF token parameter, which helps to prevent CSRF (Cross-Site Request Forgery) attack. So, it may be vulnerable to CSRF.

It send a POST request to `/my-account/change-email`, with parameter `email`, `submit`.

**Change request method to GET**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/740b8a54-220d-463a-8313-c8e9c2486ef8/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UENM3UAL%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215459Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIGNW%2B6XlS8gqFirtnnLUVTdXXNi8PnvxiW1h4FdlbyO8AiBqb986u3Na4DpecKU1rydMx8u2lmgJzQYie%2BjPwAlcfCqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMXYFA15qNoYL4wMRjKtwD%2F2Nxqvbvqq6ZAeWHMddzDTSTw%2Fw3N8PxJRYizMqOLKLT5CutQ%2B6NNHu87qfeqsAmYwIGN%2FrSSYQ9yt7jrF0bJErOXmW%2B1aliQtCei9sbK%2FfSA%2Fv0spEyDtq9jVFm8R3HV8kbQlx1ayvOGFF40ULF%2F8yGV%2BsmpQyHgU9NdLr%2FDL2d14NuNJfg3G4xYIWdLi3uWmfI%2BdX%2FP%2BPH8ujPyBO%2FvBG9XHUxsZeB6iEHyu4h7Z2XSa85MBD%2FAF%2FuFUErV8AsHk1zSwiINGnWuL%2FeWCNls14jKYZILXTzQci7OIXEyUesYfOotlR6iOctKWXZfaiX50Zrwp7CevCTwGo9rYSIr2oL%2BS6UEUsg61gvgoLYlrcFI05GfmzKaE9PserMdi5t%2BsYFx7MMm1N2%2FSaHnOeDtCb1tQWbTvpCAIVdXeR%2FcBaB%2FQB0NwA4aGdJ9TxvmXfBfzOFdD1umkHj4zdLaHPBN8xMpZp1i6DBjtsTCaqhf6IeiX%2FYeJX5MrsVzTE9O9ZcFJ22XOcjBW12ZtjuTbUAoVJV7ky82VKHFgMuiQtGcvz9yO9bzdSIg%2FT6txtCG3sLMuNwCha9P9PY3%2BUXe8oH1v7LfBIpcmOyycIChH6DM46M7DHrOtXV3RlPSz0wmIaj1AY6pgHn4h2Lg5%2FiaVBLun9yfn3fpDmmswj6xCIckQtZaOpqjnANvahR3TpP9kSGnF7%2FvyUbsnV3447TxNH%2FXPdUIFEeYR6QlGqGbzPv9v9KK2BuhV3oSHDPtGWI%2F4sWlxGkiur1jUnOcKlfjuhgZAtubu0DTDxijlCVpnkvGAhV6Gg%2FySqdsUvotse75qjT7y9lwmlfFOtMCRXIzJyXAYzcBymRBI0Hq4WD&X-Amz-Signature=9ad5fa9c9a5549dc8425a03e1f9d5baf5cbd157a7185183d9e551c2aeca00c92&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

It accepts the GET method too

However, in order to exploit CSRF, we first have to **bypass the **`SameSite=Strict`** restriction.**

> 💡 **Strict restriction:**

If a cookie is set with the `SameSite=Strict `attribute, browsers won’t include it in any cross-site requests. You may be able to get around this limitation if you can find a gadget that results in a secondary request within the same site.

One possible gadget is a client-side redirect that dynamically constructs the redirection target using attacker-controllable input like URL parameters.

As far as browsers are concerned, these client-side redirects aren’t really redirects at all; the resulting request is just treated as an ordinary, standalone request. Most importantly, this is a same-site request and, as such, will include all cookies related to the site, regardless of any restrictions that are in place.

If you can manipulate this gadget to elicit a malicious secondary request, this can enable you to bypass any SameSite cookie restrictions completely.

**Find & Understand the Client Side Redirect**

In the home page, we can view different posts And we can leave some comments.

Let’s leave a test comment:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/62aa176a-6c07-414a-99c8-2dbe3de596c9/2024-02-23_00-31.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UENM3UAL%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215459Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIGNW%2B6XlS8gqFirtnnLUVTdXXNi8PnvxiW1h4FdlbyO8AiBqb986u3Na4DpecKU1rydMx8u2lmgJzQYie%2BjPwAlcfCqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMXYFA15qNoYL4wMRjKtwD%2F2Nxqvbvqq6ZAeWHMddzDTSTw%2Fw3N8PxJRYizMqOLKLT5CutQ%2B6NNHu87qfeqsAmYwIGN%2FrSSYQ9yt7jrF0bJErOXmW%2B1aliQtCei9sbK%2FfSA%2Fv0spEyDtq9jVFm8R3HV8kbQlx1ayvOGFF40ULF%2F8yGV%2BsmpQyHgU9NdLr%2FDL2d14NuNJfg3G4xYIWdLi3uWmfI%2BdX%2FP%2BPH8ujPyBO%2FvBG9XHUxsZeB6iEHyu4h7Z2XSa85MBD%2FAF%2FuFUErV8AsHk1zSwiINGnWuL%2FeWCNls14jKYZILXTzQci7OIXEyUesYfOotlR6iOctKWXZfaiX50Zrwp7CevCTwGo9rYSIr2oL%2BS6UEUsg61gvgoLYlrcFI05GfmzKaE9PserMdi5t%2BsYFx7MMm1N2%2FSaHnOeDtCb1tQWbTvpCAIVdXeR%2FcBaB%2FQB0NwA4aGdJ9TxvmXfBfzOFdD1umkHj4zdLaHPBN8xMpZp1i6DBjtsTCaqhf6IeiX%2FYeJX5MrsVzTE9O9ZcFJ22XOcjBW12ZtjuTbUAoVJV7ky82VKHFgMuiQtGcvz9yO9bzdSIg%2FT6txtCG3sLMuNwCha9P9PY3%2BUXe8oH1v7LfBIpcmOyycIChH6DM46M7DHrOtXV3RlPSz0wmIaj1AY6pgHn4h2Lg5%2FiaVBLun9yfn3fpDmmswj6xCIckQtZaOpqjnANvahR3TpP9kSGnF7%2FvyUbsnV3447TxNH%2FXPdUIFEeYR6QlGqGbzPv9v9KK2BuhV3oSHDPtGWI%2F4sWlxGkiur1jUnOcKlfjuhgZAtubu0DTDxijlCVpnkvGAhV6Gg%2FySqdsUvotse75qjT7y9lwmlfFOtMCRXIzJyXAYzcBymRBI0Hq4WD&X-Amz-Signature=2a1be67965bc1b1bcfeb0f8043f9d6b10651dea691bd374200bcdafde9f89d39&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/0893e271-ef59-4e3a-8280-b06cd6ea63d2/2024-02-22_21-23.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UENM3UAL%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215459Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIGNW%2B6XlS8gqFirtnnLUVTdXXNi8PnvxiW1h4FdlbyO8AiBqb986u3Na4DpecKU1rydMx8u2lmgJzQYie%2BjPwAlcfCqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMXYFA15qNoYL4wMRjKtwD%2F2Nxqvbvqq6ZAeWHMddzDTSTw%2Fw3N8PxJRYizMqOLKLT5CutQ%2B6NNHu87qfeqsAmYwIGN%2FrSSYQ9yt7jrF0bJErOXmW%2B1aliQtCei9sbK%2FfSA%2Fv0spEyDtq9jVFm8R3HV8kbQlx1ayvOGFF40ULF%2F8yGV%2BsmpQyHgU9NdLr%2FDL2d14NuNJfg3G4xYIWdLi3uWmfI%2BdX%2FP%2BPH8ujPyBO%2FvBG9XHUxsZeB6iEHyu4h7Z2XSa85MBD%2FAF%2FuFUErV8AsHk1zSwiINGnWuL%2FeWCNls14jKYZILXTzQci7OIXEyUesYfOotlR6iOctKWXZfaiX50Zrwp7CevCTwGo9rYSIr2oL%2BS6UEUsg61gvgoLYlrcFI05GfmzKaE9PserMdi5t%2BsYFx7MMm1N2%2FSaHnOeDtCb1tQWbTvpCAIVdXeR%2FcBaB%2FQB0NwA4aGdJ9TxvmXfBfzOFdD1umkHj4zdLaHPBN8xMpZp1i6DBjtsTCaqhf6IeiX%2FYeJX5MrsVzTE9O9ZcFJ22XOcjBW12ZtjuTbUAoVJV7ky82VKHFgMuiQtGcvz9yO9bzdSIg%2FT6txtCG3sLMuNwCha9P9PY3%2BUXe8oH1v7LfBIpcmOyycIChH6DM46M7DHrOtXV3RlPSz0wmIaj1AY6pgHn4h2Lg5%2FiaVBLun9yfn3fpDmmswj6xCIckQtZaOpqjnANvahR3TpP9kSGnF7%2FvyUbsnV3447TxNH%2FXPdUIFEeYR6QlGqGbzPv9v9KK2BuhV3oSHDPtGWI%2F4sWlxGkiur1jUnOcKlfjuhgZAtubu0DTDxijlCVpnkvGAhV6Gg%2FySqdsUvotse75qjT7y9lwmlfFOtMCRXIzJyXAYzcBymRBI0Hq4WD&X-Amz-Signature=50864dadf3524546ef15c8a8ab6adbf32557abb7abdcf74742edb79249b98b49&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

After we send the request, it’ll fetch a JavaScript file:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/fb9ef1eb-a927-412b-96dc-23e4328e074a/2024-02-23_00-32.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UENM3UAL%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215459Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIGNW%2B6XlS8gqFirtnnLUVTdXXNi8PnvxiW1h4FdlbyO8AiBqb986u3Na4DpecKU1rydMx8u2lmgJzQYie%2BjPwAlcfCqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMXYFA15qNoYL4wMRjKtwD%2F2Nxqvbvqq6ZAeWHMddzDTSTw%2Fw3N8PxJRYizMqOLKLT5CutQ%2B6NNHu87qfeqsAmYwIGN%2FrSSYQ9yt7jrF0bJErOXmW%2B1aliQtCei9sbK%2FfSA%2Fv0spEyDtq9jVFm8R3HV8kbQlx1ayvOGFF40ULF%2F8yGV%2BsmpQyHgU9NdLr%2FDL2d14NuNJfg3G4xYIWdLi3uWmfI%2BdX%2FP%2BPH8ujPyBO%2FvBG9XHUxsZeB6iEHyu4h7Z2XSa85MBD%2FAF%2FuFUErV8AsHk1zSwiINGnWuL%2FeWCNls14jKYZILXTzQci7OIXEyUesYfOotlR6iOctKWXZfaiX50Zrwp7CevCTwGo9rYSIr2oL%2BS6UEUsg61gvgoLYlrcFI05GfmzKaE9PserMdi5t%2BsYFx7MMm1N2%2FSaHnOeDtCb1tQWbTvpCAIVdXeR%2FcBaB%2FQB0NwA4aGdJ9TxvmXfBfzOFdD1umkHj4zdLaHPBN8xMpZp1i6DBjtsTCaqhf6IeiX%2FYeJX5MrsVzTE9O9ZcFJ22XOcjBW12ZtjuTbUAoVJV7ky82VKHFgMuiQtGcvz9yO9bzdSIg%2FT6txtCG3sLMuNwCha9P9PY3%2BUXe8oH1v7LfBIpcmOyycIChH6DM46M7DHrOtXV3RlPSz0wmIaj1AY6pgHn4h2Lg5%2FiaVBLun9yfn3fpDmmswj6xCIckQtZaOpqjnANvahR3TpP9kSGnF7%2FvyUbsnV3447TxNH%2FXPdUIFEeYR6QlGqGbzPv9v9KK2BuhV3oSHDPtGWI%2F4sWlxGkiur1jUnOcKlfjuhgZAtubu0DTDxijlCVpnkvGAhV6Gg%2FySqdsUvotse75qjT7y9lwmlfFOtMCRXIzJyXAYzcBymRBI0Hq4WD&X-Amz-Signature=c1b634cceeca5ff8842a0bf83c43180a71cdb0a39ecc5f8002fdfc465747a493&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

When we go to `/post/comment/confirmation`, it’ll run that JavaScript:

- After 3 seconds, redirect user to `/post/<postId>`

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/96991d29-353c-4165-9378-acf6cd0d9507/2024-02-22_21-25.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UENM3UAL%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215459Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIGNW%2B6XlS8gqFirtnnLUVTdXXNi8PnvxiW1h4FdlbyO8AiBqb986u3Na4DpecKU1rydMx8u2lmgJzQYie%2BjPwAlcfCqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMXYFA15qNoYL4wMRjKtwD%2F2Nxqvbvqq6ZAeWHMddzDTSTw%2Fw3N8PxJRYizMqOLKLT5CutQ%2B6NNHu87qfeqsAmYwIGN%2FrSSYQ9yt7jrF0bJErOXmW%2B1aliQtCei9sbK%2FfSA%2Fv0spEyDtq9jVFm8R3HV8kbQlx1ayvOGFF40ULF%2F8yGV%2BsmpQyHgU9NdLr%2FDL2d14NuNJfg3G4xYIWdLi3uWmfI%2BdX%2FP%2BPH8ujPyBO%2FvBG9XHUxsZeB6iEHyu4h7Z2XSa85MBD%2FAF%2FuFUErV8AsHk1zSwiINGnWuL%2FeWCNls14jKYZILXTzQci7OIXEyUesYfOotlR6iOctKWXZfaiX50Zrwp7CevCTwGo9rYSIr2oL%2BS6UEUsg61gvgoLYlrcFI05GfmzKaE9PserMdi5t%2BsYFx7MMm1N2%2FSaHnOeDtCb1tQWbTvpCAIVdXeR%2FcBaB%2FQB0NwA4aGdJ9TxvmXfBfzOFdD1umkHj4zdLaHPBN8xMpZp1i6DBjtsTCaqhf6IeiX%2FYeJX5MrsVzTE9O9ZcFJ22XOcjBW12ZtjuTbUAoVJV7ky82VKHFgMuiQtGcvz9yO9bzdSIg%2FT6txtCG3sLMuNwCha9P9PY3%2BUXe8oH1v7LfBIpcmOyycIChH6DM46M7DHrOtXV3RlPSz0wmIaj1AY6pgHn4h2Lg5%2FiaVBLun9yfn3fpDmmswj6xCIckQtZaOpqjnANvahR3TpP9kSGnF7%2FvyUbsnV3447TxNH%2FXPdUIFEeYR6QlGqGbzPv9v9KK2BuhV3oSHDPtGWI%2F4sWlxGkiur1jUnOcKlfjuhgZAtubu0DTDxijlCVpnkvGAhV6Gg%2FySqdsUvotse75qjT7y9lwmlfFOtMCRXIzJyXAYzcBymRBI0Hq4WD&X-Amz-Signature=3e8f8028d897c45125ce6e0cf343c1376ff91ea3793c18b3eb305a3414c08c3c&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

However, the GET parameter `postId` is fully under attacker’s control!

**Now, what if I change the path to **`/my-account`** via path traversal?**

- Start crafting our payload

```html
/post/comment/confirmation?postId=6
```

- Change payload to redirect to my-account page

```html
/post/comment/confirmation?postId=my-account/
```

- Add a traversal attack to our payload

```html
/post/comment/confirmation?postId=../my-account/
```

- Modify payload to change our email

```html
/post/comment/confirmation?postId=../my-account/change-email?email=test@wiener.com&submit=1
```

- URL encode ampersand `&` may its not able to determine when our mail ends

```html
/post/comment/confirmation?postId=../my-account/change-email?email=test@wiener.com%26submit=1
```

- Craft out final payload

```html
<script>
window. location = "https://0ad1003704e4d04e8077d6250056008f.web-security-academy.net/post/comment/confirmation?postId=../my-account/change-email?email=test@wiener.com%26submit=1
</script>
```

- Deliver our final payload to the victim
