# Web shell upload via extension blacklist bypass

### Goal - 

To solve the lab, upload a basic PHP web shell and use it to exfiltrate the contents of the file `/home/carlos/secret`

### Analysis/Exploitation -

[Solution  (the easy and unintended way)](https://app.notion.com/p/8133e72ab08a41068a99f5712ad2385b#7008774cb9ca462e9cd076d4095ef174) 

Login as user `wiener`:

In the account settings, I can set both an email address and an avatar image for the user.

upload the PHP script  
`<?php system($_GET['cmd']); ?>`

Trying to upload the php script shows that PHP files are not allowed to upload:

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/6255eea3-0949-47c4-84bd-c5ea9289511b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466RT3LLOE6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204708Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDXqw56kVNggwajoBgVbx0meAai3kHx7L6LufCdUPk1rAIhAIhxPurhxOUjZJuVuju%2BmcTdxrIAv8ArmWU5fXfqsWy%2BKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igxlo%2BUHrkxSOo6bFLAq3AOFS%2FA3uMiyEai4MuWeJ9p%2BUgulgHqjIdXz0%2BPYR%2FFu16XkkzHg6oG6uf0UqGGJYZtwGRFSmaOT7E1VSpuQuJle%2FBbgrCe3uRyWu2J72x6LKipI9qc0EGv4qc9S6eNiyCWZSjdjgBLX13DMrexowxfGyQ740olafRRnZAsDNyURAOoTd%2B%2Fzf86off0yif84ldnQEJdHaa51iXpLsrIHr7GWUlde3%2FenBcSydNICdGs0gmOgtdh6ICciS22Uyig0YLSwkQkybsYN%2F5oV2lNL7vVfsFVgND6M74mKbGJXHsdeSnr33LSPnDJrHSKSZ%2Ft6teAVbpZiRWrIEPwxMXcUyV1Ym7K88Iq4x0E7QHsDM2b%2FdGl9R6EXgRREO%2BNe3gTKLxZQdWgbeojXyU2a15Z0RY2ItfttXTuCV9rbU6S2H2wZBMb10n89tK20ULFqmG3CWRT0cwNaj%2BhVn9azR92QvTbY2umzTNG%2FOkcA5qMeqhz02QJzSykklhwUanvl%2BWk%2B0KTrelYlKxUJaeITbTP3MLKc7WXelEwFij42t73zBT5xR9SgQVswBPJLCBOszQbzIULpDJoFPneqRZ9dk%2BoMgnl95tZySSGa7HmBXpWitqxP6QnmF1q%2FtrGQssinwTDlxqLUBjqkAfONMEjIWF0JAij5RAQTvnLsupAcbqiSZQ8ULrkzEnkQ9aVrsMYhHv4%2FtkcGeRBMtCkpKnMfN7Ot6Y0O4xsztiX%2B0vpiQHczJFs3dj2ZvTa5L7H5pDCBCtjDsjAOP8h4gbOB5ciO%2FjyltyvpbH2xRA5q8eaIkXpP7cp3V2inrbXZhKVx%2FcSqlRv4ejnZeSzQP0i17WiUrFGY2gdo%2BY3lFGyA5BFo&X-Amz-Signature=e65f3faeb8728788c688097b85104a620b97a27d5e67644bef8fc027ec69eb5c&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

No file with a PHP extension can be uploaded on the server. Attempts to circumvent this with different capitalization `shell.pHP` or null bytes in the filename `shell.php%00.png` showed no success.

The next step was to try some common alternative extensions for PHP files. The [hacktricks.xyz](https://book.hacktricks.xyz/pentesting-web/file-upload) list a couple of such alternatives for PHP: `phtml, .php, .php3, .php4, .php5`

To bypass this, we can rename the file extension to `.php5`. This extension tells the web server to use PHP version 5.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/7db30d74-5e6c-4e48-a2c6-385808857d7d/2024-03-01_07-57.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466RT3LLOE6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204708Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDXqw56kVNggwajoBgVbx0meAai3kHx7L6LufCdUPk1rAIhAIhxPurhxOUjZJuVuju%2BmcTdxrIAv8ArmWU5fXfqsWy%2BKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igxlo%2BUHrkxSOo6bFLAq3AOFS%2FA3uMiyEai4MuWeJ9p%2BUgulgHqjIdXz0%2BPYR%2FFu16XkkzHg6oG6uf0UqGGJYZtwGRFSmaOT7E1VSpuQuJle%2FBbgrCe3uRyWu2J72x6LKipI9qc0EGv4qc9S6eNiyCWZSjdjgBLX13DMrexowxfGyQ740olafRRnZAsDNyURAOoTd%2B%2Fzf86off0yif84ldnQEJdHaa51iXpLsrIHr7GWUlde3%2FenBcSydNICdGs0gmOgtdh6ICciS22Uyig0YLSwkQkybsYN%2F5oV2lNL7vVfsFVgND6M74mKbGJXHsdeSnr33LSPnDJrHSKSZ%2Ft6teAVbpZiRWrIEPwxMXcUyV1Ym7K88Iq4x0E7QHsDM2b%2FdGl9R6EXgRREO%2BNe3gTKLxZQdWgbeojXyU2a15Z0RY2ItfttXTuCV9rbU6S2H2wZBMb10n89tK20ULFqmG3CWRT0cwNaj%2BhVn9azR92QvTbY2umzTNG%2FOkcA5qMeqhz02QJzSykklhwUanvl%2BWk%2B0KTrelYlKxUJaeITbTP3MLKc7WXelEwFij42t73zBT5xR9SgQVswBPJLCBOszQbzIULpDJoFPneqRZ9dk%2BoMgnl95tZySSGa7HmBXpWitqxP6QnmF1q%2FtrGQssinwTDlxqLUBjqkAfONMEjIWF0JAij5RAQTvnLsupAcbqiSZQ8ULrkzEnkQ9aVrsMYhHv4%2FtkcGeRBMtCkpKnMfN7Ot6Y0O4xsztiX%2B0vpiQHczJFs3dj2ZvTa5L7H5pDCBCtjDsjAOP8h4gbOB5ciO%2FjyltyvpbH2xRA5q8eaIkXpP7cp3V2inrbXZhKVx%2FcSqlRv4ejnZeSzQP0i17WiUrFGY2gdo%2BY3lFGyA5BFo&X-Amz-Signature=0b2485f5583178c99f919fec8477cd10da328b6aeebc73f3a925df1bd7e3efc5&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

We’ve successfully uploaded the web shell!

**Check Can we execute any command?**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/9d20721b-088c-465c-855d-c047a2298ef0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466RT3LLOE6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204708Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDXqw56kVNggwajoBgVbx0meAai3kHx7L6LufCdUPk1rAIhAIhxPurhxOUjZJuVuju%2BmcTdxrIAv8ArmWU5fXfqsWy%2BKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igxlo%2BUHrkxSOo6bFLAq3AOFS%2FA3uMiyEai4MuWeJ9p%2BUgulgHqjIdXz0%2BPYR%2FFu16XkkzHg6oG6uf0UqGGJYZtwGRFSmaOT7E1VSpuQuJle%2FBbgrCe3uRyWu2J72x6LKipI9qc0EGv4qc9S6eNiyCWZSjdjgBLX13DMrexowxfGyQ740olafRRnZAsDNyURAOoTd%2B%2Fzf86off0yif84ldnQEJdHaa51iXpLsrIHr7GWUlde3%2FenBcSydNICdGs0gmOgtdh6ICciS22Uyig0YLSwkQkybsYN%2F5oV2lNL7vVfsFVgND6M74mKbGJXHsdeSnr33LSPnDJrHSKSZ%2Ft6teAVbpZiRWrIEPwxMXcUyV1Ym7K88Iq4x0E7QHsDM2b%2FdGl9R6EXgRREO%2BNe3gTKLxZQdWgbeojXyU2a15Z0RY2ItfttXTuCV9rbU6S2H2wZBMb10n89tK20ULFqmG3CWRT0cwNaj%2BhVn9azR92QvTbY2umzTNG%2FOkcA5qMeqhz02QJzSykklhwUanvl%2BWk%2B0KTrelYlKxUJaeITbTP3MLKc7WXelEwFij42t73zBT5xR9SgQVswBPJLCBOszQbzIULpDJoFPneqRZ9dk%2BoMgnl95tZySSGa7HmBXpWitqxP6QnmF1q%2FtrGQssinwTDlxqLUBjqkAfONMEjIWF0JAij5RAQTvnLsupAcbqiSZQ8ULrkzEnkQ9aVrsMYhHv4%2FtkcGeRBMtCkpKnMfN7Ot6Y0O4xsztiX%2B0vpiQHczJFs3dj2ZvTa5L7H5pDCBCtjDsjAOP8h4gbOB5ciO%2FjyltyvpbH2xRA5q8eaIkXpP7cp3V2inrbXZhKVx%2FcSqlRv4ejnZeSzQP0i17WiUrFGY2gdo%2BY3lFGyA5BFo&X-Amz-Signature=537c7dfe17392a3ade0934e2607b4d289b436114a87e1ae13bd4479f45334365&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Nope we get plain text of webShell we uploaded.This might happen is because **servers typically won’t execute files unless they have been configured to do so.**

In FireFox extension `Wappalyzer`, it will tell us which web server is using:

![](https://raw.githubusercontent.com/siunam321/CTF-Writeups/main/Portswigger-Labs/File-Upload-Vulnerabilities/FUV-4/images/Pasted%20image%2020221216012534.png)

In this case, **the web server is using **`Apache`**.**

> 💡 **In Apache server, before executing PHP files requested by a client, developers might have to add the following directives to their **`/etc/apache2/apache2.conf`** file:**

```text
LoadModule php_module /usr/lib/apache2/modules/libphp.so
AddType application/x-httpd-php .php
```

Many servers also allow developers to create special configuration files within individual directories in order to override or add to one or more of the global settings.

In Apache servers, it will load a directory-specific configuration from a file called `.htaccess` if one is present.

Now, what if I upload a file called `.htaccess` to override the server configuration?

**After poking around, I found this **[**Medium blog**](https://asreshashank.medium.com/execute-php-scripts-into-html-file-by-modifying-htaccess-file-8517ed1e2066)**:**

![](https://raw.githubusercontent.com/siunam321/CTF-Writeups/main/Portswigger-Labs/File-Upload-Vulnerabilities/FUV-4/images/Pasted%20image%2020221216013635.png)

we can create our own `.htaccess` with the following configuration:

> `AddType application/x-httpd-php .php5`

**By doing that, we can execute any file that has **`.php5`** extension!**

while uploading intercept the request and **Change the **`Content-Type`** to **`text/plain`**:**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/7da44160-911a-4b1a-9d8a-08b467fa0cc0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466RT3LLOE6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204708Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDXqw56kVNggwajoBgVbx0meAai3kHx7L6LufCdUPk1rAIhAIhxPurhxOUjZJuVuju%2BmcTdxrIAv8ArmWU5fXfqsWy%2BKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igxlo%2BUHrkxSOo6bFLAq3AOFS%2FA3uMiyEai4MuWeJ9p%2BUgulgHqjIdXz0%2BPYR%2FFu16XkkzHg6oG6uf0UqGGJYZtwGRFSmaOT7E1VSpuQuJle%2FBbgrCe3uRyWu2J72x6LKipI9qc0EGv4qc9S6eNiyCWZSjdjgBLX13DMrexowxfGyQ740olafRRnZAsDNyURAOoTd%2B%2Fzf86off0yif84ldnQEJdHaa51iXpLsrIHr7GWUlde3%2FenBcSydNICdGs0gmOgtdh6ICciS22Uyig0YLSwkQkybsYN%2F5oV2lNL7vVfsFVgND6M74mKbGJXHsdeSnr33LSPnDJrHSKSZ%2Ft6teAVbpZiRWrIEPwxMXcUyV1Ym7K88Iq4x0E7QHsDM2b%2FdGl9R6EXgRREO%2BNe3gTKLxZQdWgbeojXyU2a15Z0RY2ItfttXTuCV9rbU6S2H2wZBMb10n89tK20ULFqmG3CWRT0cwNaj%2BhVn9azR92QvTbY2umzTNG%2FOkcA5qMeqhz02QJzSykklhwUanvl%2BWk%2B0KTrelYlKxUJaeITbTP3MLKc7WXelEwFij42t73zBT5xR9SgQVswBPJLCBOszQbzIULpDJoFPneqRZ9dk%2BoMgnl95tZySSGa7HmBXpWitqxP6QnmF1q%2FtrGQssinwTDlxqLUBjqkAfONMEjIWF0JAij5RAQTvnLsupAcbqiSZQ8ULrkzEnkQ9aVrsMYhHv4%2FtkcGeRBMtCkpKnMfN7Ot6Y0O4xsztiX%2B0vpiQHczJFs3dj2ZvTa5L7H5pDCBCtjDsjAOP8h4gbOB5ciO%2FjyltyvpbH2xRA5q8eaIkXpP7cp3V2inrbXZhKVx%2FcSqlRv4ejnZeSzQP0i17WiUrFGY2gdo%2BY3lFGyA5BFo&X-Amz-Signature=ddde8f73f504ab256cf1699272a858da2c478f9dcac3005de63239452cfad3b2&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Or it can be directly uploaded from Burp Repeater, by sending  `POST /my-account/avatar` request that was used to submit the file upload.Make the following changes:

- Change the value of the `filename` parameter to `.htaccess`.
- Change the value of the `Content-Type` header to `text/plain`.
- Replace the contents of the file (your PHP payload) with the following Apache directive: `AddType application/x-httpd-php .php5`
> 💡 I noticed that I was able to upload a number of different file extension, possibly even arbitrary ones like `.a2z, .abc` .

If reusing an upload request of `png` or `php` files for the Repeater it is important to set the Content-Type to `text/plain`. Otherwise, the server will return a `500 Internal Server error` when trying to load something later on.

The application is served by an apache server, so uploading a custom .htaccess file maps an arbitrary extension (`.a2z`) to the executable MIME type `application/x-httpd-php`. As the server uses the `mod_php` module, it knows how to handle this already.

now we can execute command                                             

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/d35ddc09-b43d-40d8-a145-c24c4978f3d5/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466RT3LLOE6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204708Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDXqw56kVNggwajoBgVbx0meAai3kHx7L6LufCdUPk1rAIhAIhxPurhxOUjZJuVuju%2BmcTdxrIAv8ArmWU5fXfqsWy%2BKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igxlo%2BUHrkxSOo6bFLAq3AOFS%2FA3uMiyEai4MuWeJ9p%2BUgulgHqjIdXz0%2BPYR%2FFu16XkkzHg6oG6uf0UqGGJYZtwGRFSmaOT7E1VSpuQuJle%2FBbgrCe3uRyWu2J72x6LKipI9qc0EGv4qc9S6eNiyCWZSjdjgBLX13DMrexowxfGyQ740olafRRnZAsDNyURAOoTd%2B%2Fzf86off0yif84ldnQEJdHaa51iXpLsrIHr7GWUlde3%2FenBcSydNICdGs0gmOgtdh6ICciS22Uyig0YLSwkQkybsYN%2F5oV2lNL7vVfsFVgND6M74mKbGJXHsdeSnr33LSPnDJrHSKSZ%2Ft6teAVbpZiRWrIEPwxMXcUyV1Ym7K88Iq4x0E7QHsDM2b%2FdGl9R6EXgRREO%2BNe3gTKLxZQdWgbeojXyU2a15Z0RY2ItfttXTuCV9rbU6S2H2wZBMb10n89tK20ULFqmG3CWRT0cwNaj%2BhVn9azR92QvTbY2umzTNG%2FOkcA5qMeqhz02QJzSykklhwUanvl%2BWk%2B0KTrelYlKxUJaeITbTP3MLKc7WXelEwFij42t73zBT5xR9SgQVswBPJLCBOszQbzIULpDJoFPneqRZ9dk%2BoMgnl95tZySSGa7HmBXpWitqxP6QnmF1q%2FtrGQssinwTDlxqLUBjqkAfONMEjIWF0JAij5RAQTvnLsupAcbqiSZQ8ULrkzEnkQ9aVrsMYhHv4%2FtkcGeRBMtCkpKnMfN7Ot6Y0O4xsztiX%2B0vpiQHczJFs3dj2ZvTa5L7H5pDCBCtjDsjAOP8h4gbOB5ciO%2FjyltyvpbH2xRA5q8eaIkXpP7cp3V2inrbXZhKVx%2FcSqlRv4ejnZeSzQP0i17WiUrFGY2gdo%2BY3lFGyA5BFo&X-Amz-Signature=9dcea23ccb0b11d310e5af7c116ebd451b6d582f3e175218adc8034c4eeeb580&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Fetch the carlos secret

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/73346238-3276-4754-9349-8bd022136e88/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466RT3LLOE6%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204708Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDXqw56kVNggwajoBgVbx0meAai3kHx7L6LufCdUPk1rAIhAIhxPurhxOUjZJuVuju%2BmcTdxrIAv8ArmWU5fXfqsWy%2BKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igxlo%2BUHrkxSOo6bFLAq3AOFS%2FA3uMiyEai4MuWeJ9p%2BUgulgHqjIdXz0%2BPYR%2FFu16XkkzHg6oG6uf0UqGGJYZtwGRFSmaOT7E1VSpuQuJle%2FBbgrCe3uRyWu2J72x6LKipI9qc0EGv4qc9S6eNiyCWZSjdjgBLX13DMrexowxfGyQ740olafRRnZAsDNyURAOoTd%2B%2Fzf86off0yif84ldnQEJdHaa51iXpLsrIHr7GWUlde3%2FenBcSydNICdGs0gmOgtdh6ICciS22Uyig0YLSwkQkybsYN%2F5oV2lNL7vVfsFVgND6M74mKbGJXHsdeSnr33LSPnDJrHSKSZ%2Ft6teAVbpZiRWrIEPwxMXcUyV1Ym7K88Iq4x0E7QHsDM2b%2FdGl9R6EXgRREO%2BNe3gTKLxZQdWgbeojXyU2a15Z0RY2ItfttXTuCV9rbU6S2H2wZBMb10n89tK20ULFqmG3CWRT0cwNaj%2BhVn9azR92QvTbY2umzTNG%2FOkcA5qMeqhz02QJzSykklhwUanvl%2BWk%2B0KTrelYlKxUJaeITbTP3MLKc7WXelEwFij42t73zBT5xR9SgQVswBPJLCBOszQbzIULpDJoFPneqRZ9dk%2BoMgnl95tZySSGa7HmBXpWitqxP6QnmF1q%2FtrGQssinwTDlxqLUBjqkAfONMEjIWF0JAij5RAQTvnLsupAcbqiSZQ8ULrkzEnkQ9aVrsMYhHv4%2FtkcGeRBMtCkpKnMfN7Ot6Y0O4xsztiX%2B0vpiQHczJFs3dj2ZvTa5L7H5pDCBCtjDsjAOP8h4gbOB5ciO%2FjyltyvpbH2xRA5q8eaIkXpP7cp3V2inrbXZhKVx%2FcSqlRv4ejnZeSzQP0i17WiUrFGY2gdo%2BY3lFGyA5BFo&X-Amz-Signature=e1c70287d6079345c6c8c58774a371d271e345324b1df5747f89fe0bdf8bf3da&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)


### **Solution  (the easy and unintended way)**

While the extensions with numbers at the end uploaded successful, they were not executed by the server. Uploading and accessing the file as `.phtml` is a different story and executes the script:

![](https://github.com/frank-leitner/portswigger-websecurity-academy/raw/main/08_file_upload_vulnerabilities/Web_shell_upload_via_extension_blacklist_bypass/img/phtml_solution.png)
