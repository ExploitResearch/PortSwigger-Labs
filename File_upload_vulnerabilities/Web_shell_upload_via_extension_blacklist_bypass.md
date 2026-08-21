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

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/6255eea3-0949-47c4-84bd-c5ea9289511b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4663YR4QTRG%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215544Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDfVAoueMr7h1L4zemjb5CMI0lCWRsLgZ56lJwflYGptgIgO0ElzO%2B%2F1JKdJO2klmShzWBRV3j0RqwCqT29oIgT7%2FAqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDGqOrc7QXc0kqV6bkircA3LdtxBQtvjMyWFcOddmYmVQxr7XsRVzwiF8QOGkiiseUgogkDRPEiaFtymBpEHfOFb2Z5%2FP%2FSg1QjdMJK874Vn2GY46qJPmBQOIRX1FAvNG9mapO5cUILpesT%2BxXcrfh%2BAxB%2B%2BAYiwPTjmzfLs9WiM6EdMI3E4f4gZEHj6LIuZgeq7a9qxe69XSYUermLors1ZcR0ojbsjbU5u9nWb%2BeeaC5UWnMt5T4QY9qs5s8iO4ftVPxBO8iPO2Gkm1i9FQnpkYo3EwTWpuMbLSXRUd%2BQ%2Bw%2FASO00nYCeJr8RSOU7nnvBEg3uENIIc6UiK164qjoi4DI9eqvqmFWDmDjmkQBKYNRzkQw3OjTzTYAvOm64X3RQ1OfW0%2F2GxSJwgIYwZl4fEA8Iq%2B8PvpIVZGmpWeGss%2FeWa7SvaCkpLytQ7Veu4IUdINgKtPBMLYfcyHbEZoidQKJ%2FQm9vt1MP%2Fpq6F%2BVNbohuGFpsPsojtWtG%2BWh4wLwNnHU1BvXOn50pRGcZ%2FXM%2BTrRLiFWDhSXpNVWZ%2Boik%2FE6i3zanFhD5AYfNrjRcIdP%2By7HVsL2gJfMpiNPc4vx4%2BqxlM8R6kg%2FCtk5HQKL5k3Rjc5Nb8MAtMyukKkFj21SwguVZ%2BUtrfgLJYyMI6Ho9QGOqUBLgnmlSpug%2FzoPjaxhm5a2h1BhMhwqIMjq8fU%2FP1C2HE%2FDaFpw1OPyQZ80kv6qLbRx3cDrWbA6i8r0%2BPLR9VBJRaJxq46JEON%2BoS%2BeksAWf7ygMvEXkucGJqpMJHZPW2lrnnbSVXgwi%2BQPuLP7FznaKb%2F71z4ZM48xqPQ7%2Fiag4FO%2F5VbOypLVWqhAeEScb6FSrfNHz9WcQG%2BGj0vcVLSAsXWz%2Bkw&X-Amz-Signature=7173865ab3d83a0ee206cf2d50ae6c88366ad622296f03ef656c9da35e01bdf6&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

No file with a PHP extension can be uploaded on the server. Attempts to circumvent this with different capitalization `shell.pHP` or null bytes in the filename `shell.php%00.png` showed no success.

The next step was to try some common alternative extensions for PHP files. The [hacktricks.xyz](https://book.hacktricks.xyz/pentesting-web/file-upload) list a couple of such alternatives for PHP: `phtml, .php, .php3, .php4, .php5`

To bypass this, we can rename the file extension to `.php5`. This extension tells the web server to use PHP version 5.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/7db30d74-5e6c-4e48-a2c6-385808857d7d/2024-03-01_07-57.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4663YR4QTRG%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215544Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDfVAoueMr7h1L4zemjb5CMI0lCWRsLgZ56lJwflYGptgIgO0ElzO%2B%2F1JKdJO2klmShzWBRV3j0RqwCqT29oIgT7%2FAqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDGqOrc7QXc0kqV6bkircA3LdtxBQtvjMyWFcOddmYmVQxr7XsRVzwiF8QOGkiiseUgogkDRPEiaFtymBpEHfOFb2Z5%2FP%2FSg1QjdMJK874Vn2GY46qJPmBQOIRX1FAvNG9mapO5cUILpesT%2BxXcrfh%2BAxB%2B%2BAYiwPTjmzfLs9WiM6EdMI3E4f4gZEHj6LIuZgeq7a9qxe69XSYUermLors1ZcR0ojbsjbU5u9nWb%2BeeaC5UWnMt5T4QY9qs5s8iO4ftVPxBO8iPO2Gkm1i9FQnpkYo3EwTWpuMbLSXRUd%2BQ%2Bw%2FASO00nYCeJr8RSOU7nnvBEg3uENIIc6UiK164qjoi4DI9eqvqmFWDmDjmkQBKYNRzkQw3OjTzTYAvOm64X3RQ1OfW0%2F2GxSJwgIYwZl4fEA8Iq%2B8PvpIVZGmpWeGss%2FeWa7SvaCkpLytQ7Veu4IUdINgKtPBMLYfcyHbEZoidQKJ%2FQm9vt1MP%2Fpq6F%2BVNbohuGFpsPsojtWtG%2BWh4wLwNnHU1BvXOn50pRGcZ%2FXM%2BTrRLiFWDhSXpNVWZ%2Boik%2FE6i3zanFhD5AYfNrjRcIdP%2By7HVsL2gJfMpiNPc4vx4%2BqxlM8R6kg%2FCtk5HQKL5k3Rjc5Nb8MAtMyukKkFj21SwguVZ%2BUtrfgLJYyMI6Ho9QGOqUBLgnmlSpug%2FzoPjaxhm5a2h1BhMhwqIMjq8fU%2FP1C2HE%2FDaFpw1OPyQZ80kv6qLbRx3cDrWbA6i8r0%2BPLR9VBJRaJxq46JEON%2BoS%2BeksAWf7ygMvEXkucGJqpMJHZPW2lrnnbSVXgwi%2BQPuLP7FznaKb%2F71z4ZM48xqPQ7%2Fiag4FO%2F5VbOypLVWqhAeEScb6FSrfNHz9WcQG%2BGj0vcVLSAsXWz%2Bkw&X-Amz-Signature=332ac9c2e525c95137c25cb4130769bf7a1cf53aa2e2bf17188a6b3eb83db067&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

We’ve successfully uploaded the web shell!

**Check Can we execute any command?**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/9d20721b-088c-465c-855d-c047a2298ef0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4663YR4QTRG%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215544Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDfVAoueMr7h1L4zemjb5CMI0lCWRsLgZ56lJwflYGptgIgO0ElzO%2B%2F1JKdJO2klmShzWBRV3j0RqwCqT29oIgT7%2FAqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDGqOrc7QXc0kqV6bkircA3LdtxBQtvjMyWFcOddmYmVQxr7XsRVzwiF8QOGkiiseUgogkDRPEiaFtymBpEHfOFb2Z5%2FP%2FSg1QjdMJK874Vn2GY46qJPmBQOIRX1FAvNG9mapO5cUILpesT%2BxXcrfh%2BAxB%2B%2BAYiwPTjmzfLs9WiM6EdMI3E4f4gZEHj6LIuZgeq7a9qxe69XSYUermLors1ZcR0ojbsjbU5u9nWb%2BeeaC5UWnMt5T4QY9qs5s8iO4ftVPxBO8iPO2Gkm1i9FQnpkYo3EwTWpuMbLSXRUd%2BQ%2Bw%2FASO00nYCeJr8RSOU7nnvBEg3uENIIc6UiK164qjoi4DI9eqvqmFWDmDjmkQBKYNRzkQw3OjTzTYAvOm64X3RQ1OfW0%2F2GxSJwgIYwZl4fEA8Iq%2B8PvpIVZGmpWeGss%2FeWa7SvaCkpLytQ7Veu4IUdINgKtPBMLYfcyHbEZoidQKJ%2FQm9vt1MP%2Fpq6F%2BVNbohuGFpsPsojtWtG%2BWh4wLwNnHU1BvXOn50pRGcZ%2FXM%2BTrRLiFWDhSXpNVWZ%2Boik%2FE6i3zanFhD5AYfNrjRcIdP%2By7HVsL2gJfMpiNPc4vx4%2BqxlM8R6kg%2FCtk5HQKL5k3Rjc5Nb8MAtMyukKkFj21SwguVZ%2BUtrfgLJYyMI6Ho9QGOqUBLgnmlSpug%2FzoPjaxhm5a2h1BhMhwqIMjq8fU%2FP1C2HE%2FDaFpw1OPyQZ80kv6qLbRx3cDrWbA6i8r0%2BPLR9VBJRaJxq46JEON%2BoS%2BeksAWf7ygMvEXkucGJqpMJHZPW2lrnnbSVXgwi%2BQPuLP7FznaKb%2F71z4ZM48xqPQ7%2Fiag4FO%2F5VbOypLVWqhAeEScb6FSrfNHz9WcQG%2BGj0vcVLSAsXWz%2Bkw&X-Amz-Signature=f606e21aaa76d995d57330fc66a394f6fdc5aff09e74870960aa4bbca43377eb&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/7da44160-911a-4b1a-9d8a-08b467fa0cc0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4663YR4QTRG%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215544Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDfVAoueMr7h1L4zemjb5CMI0lCWRsLgZ56lJwflYGptgIgO0ElzO%2B%2F1JKdJO2klmShzWBRV3j0RqwCqT29oIgT7%2FAqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDGqOrc7QXc0kqV6bkircA3LdtxBQtvjMyWFcOddmYmVQxr7XsRVzwiF8QOGkiiseUgogkDRPEiaFtymBpEHfOFb2Z5%2FP%2FSg1QjdMJK874Vn2GY46qJPmBQOIRX1FAvNG9mapO5cUILpesT%2BxXcrfh%2BAxB%2B%2BAYiwPTjmzfLs9WiM6EdMI3E4f4gZEHj6LIuZgeq7a9qxe69XSYUermLors1ZcR0ojbsjbU5u9nWb%2BeeaC5UWnMt5T4QY9qs5s8iO4ftVPxBO8iPO2Gkm1i9FQnpkYo3EwTWpuMbLSXRUd%2BQ%2Bw%2FASO00nYCeJr8RSOU7nnvBEg3uENIIc6UiK164qjoi4DI9eqvqmFWDmDjmkQBKYNRzkQw3OjTzTYAvOm64X3RQ1OfW0%2F2GxSJwgIYwZl4fEA8Iq%2B8PvpIVZGmpWeGss%2FeWa7SvaCkpLytQ7Veu4IUdINgKtPBMLYfcyHbEZoidQKJ%2FQm9vt1MP%2Fpq6F%2BVNbohuGFpsPsojtWtG%2BWh4wLwNnHU1BvXOn50pRGcZ%2FXM%2BTrRLiFWDhSXpNVWZ%2Boik%2FE6i3zanFhD5AYfNrjRcIdP%2By7HVsL2gJfMpiNPc4vx4%2BqxlM8R6kg%2FCtk5HQKL5k3Rjc5Nb8MAtMyukKkFj21SwguVZ%2BUtrfgLJYyMI6Ho9QGOqUBLgnmlSpug%2FzoPjaxhm5a2h1BhMhwqIMjq8fU%2FP1C2HE%2FDaFpw1OPyQZ80kv6qLbRx3cDrWbA6i8r0%2BPLR9VBJRaJxq46JEON%2BoS%2BeksAWf7ygMvEXkucGJqpMJHZPW2lrnnbSVXgwi%2BQPuLP7FznaKb%2F71z4ZM48xqPQ7%2Fiag4FO%2F5VbOypLVWqhAeEScb6FSrfNHz9WcQG%2BGj0vcVLSAsXWz%2Bkw&X-Amz-Signature=ceca0782ecae48bad33983f9e017bc54a6994cc14f22d8bf69cda00e4f864980&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Or it can be directly uploaded from Burp Repeater, by sending  `POST /my-account/avatar` request that was used to submit the file upload.Make the following changes:

- Change the value of the `filename` parameter to `.htaccess`.
- Change the value of the `Content-Type` header to `text/plain`.
- Replace the contents of the file (your PHP payload) with the following Apache directive: `AddType application/x-httpd-php .php5`

> 💡 I noticed that I was able to upload a number of different file extension, possibly even arbitrary ones like `.a2z, .abc` .

If reusing an upload request of `png` or `php` files for the Repeater it is important to set the Content-Type to `text/plain`. Otherwise, the server will return a `500 Internal Server error` when trying to load something later on.

The application is served by an apache server, so uploading a custom .htaccess file maps an arbitrary extension (`.a2z`) to the executable MIME type `application/x-httpd-php`. As the server uses the `mod_php` module, it knows how to handle this already.

now we can execute command                                             

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/d35ddc09-b43d-40d8-a145-c24c4978f3d5/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4663YR4QTRG%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215544Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDfVAoueMr7h1L4zemjb5CMI0lCWRsLgZ56lJwflYGptgIgO0ElzO%2B%2F1JKdJO2klmShzWBRV3j0RqwCqT29oIgT7%2FAqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDGqOrc7QXc0kqV6bkircA3LdtxBQtvjMyWFcOddmYmVQxr7XsRVzwiF8QOGkiiseUgogkDRPEiaFtymBpEHfOFb2Z5%2FP%2FSg1QjdMJK874Vn2GY46qJPmBQOIRX1FAvNG9mapO5cUILpesT%2BxXcrfh%2BAxB%2B%2BAYiwPTjmzfLs9WiM6EdMI3E4f4gZEHj6LIuZgeq7a9qxe69XSYUermLors1ZcR0ojbsjbU5u9nWb%2BeeaC5UWnMt5T4QY9qs5s8iO4ftVPxBO8iPO2Gkm1i9FQnpkYo3EwTWpuMbLSXRUd%2BQ%2Bw%2FASO00nYCeJr8RSOU7nnvBEg3uENIIc6UiK164qjoi4DI9eqvqmFWDmDjmkQBKYNRzkQw3OjTzTYAvOm64X3RQ1OfW0%2F2GxSJwgIYwZl4fEA8Iq%2B8PvpIVZGmpWeGss%2FeWa7SvaCkpLytQ7Veu4IUdINgKtPBMLYfcyHbEZoidQKJ%2FQm9vt1MP%2Fpq6F%2BVNbohuGFpsPsojtWtG%2BWh4wLwNnHU1BvXOn50pRGcZ%2FXM%2BTrRLiFWDhSXpNVWZ%2Boik%2FE6i3zanFhD5AYfNrjRcIdP%2By7HVsL2gJfMpiNPc4vx4%2BqxlM8R6kg%2FCtk5HQKL5k3Rjc5Nb8MAtMyukKkFj21SwguVZ%2BUtrfgLJYyMI6Ho9QGOqUBLgnmlSpug%2FzoPjaxhm5a2h1BhMhwqIMjq8fU%2FP1C2HE%2FDaFpw1OPyQZ80kv6qLbRx3cDrWbA6i8r0%2BPLR9VBJRaJxq46JEON%2BoS%2BeksAWf7ygMvEXkucGJqpMJHZPW2lrnnbSVXgwi%2BQPuLP7FznaKb%2F71z4ZM48xqPQ7%2Fiag4FO%2F5VbOypLVWqhAeEScb6FSrfNHz9WcQG%2BGj0vcVLSAsXWz%2Bkw&X-Amz-Signature=6e77e5c88a2b4d8a89334eb9055aeadc8a7e3f4e2a31310f4fbdb83416698701&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Fetch the carlos secret

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/73346238-3276-4754-9349-8bd022136e88/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4663YR4QTRG%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215544Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDfVAoueMr7h1L4zemjb5CMI0lCWRsLgZ56lJwflYGptgIgO0ElzO%2B%2F1JKdJO2klmShzWBRV3j0RqwCqT29oIgT7%2FAqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDGqOrc7QXc0kqV6bkircA3LdtxBQtvjMyWFcOddmYmVQxr7XsRVzwiF8QOGkiiseUgogkDRPEiaFtymBpEHfOFb2Z5%2FP%2FSg1QjdMJK874Vn2GY46qJPmBQOIRX1FAvNG9mapO5cUILpesT%2BxXcrfh%2BAxB%2B%2BAYiwPTjmzfLs9WiM6EdMI3E4f4gZEHj6LIuZgeq7a9qxe69XSYUermLors1ZcR0ojbsjbU5u9nWb%2BeeaC5UWnMt5T4QY9qs5s8iO4ftVPxBO8iPO2Gkm1i9FQnpkYo3EwTWpuMbLSXRUd%2BQ%2Bw%2FASO00nYCeJr8RSOU7nnvBEg3uENIIc6UiK164qjoi4DI9eqvqmFWDmDjmkQBKYNRzkQw3OjTzTYAvOm64X3RQ1OfW0%2F2GxSJwgIYwZl4fEA8Iq%2B8PvpIVZGmpWeGss%2FeWa7SvaCkpLytQ7Veu4IUdINgKtPBMLYfcyHbEZoidQKJ%2FQm9vt1MP%2Fpq6F%2BVNbohuGFpsPsojtWtG%2BWh4wLwNnHU1BvXOn50pRGcZ%2FXM%2BTrRLiFWDhSXpNVWZ%2Boik%2FE6i3zanFhD5AYfNrjRcIdP%2By7HVsL2gJfMpiNPc4vx4%2BqxlM8R6kg%2FCtk5HQKL5k3Rjc5Nb8MAtMyukKkFj21SwguVZ%2BUtrfgLJYyMI6Ho9QGOqUBLgnmlSpug%2FzoPjaxhm5a2h1BhMhwqIMjq8fU%2FP1C2HE%2FDaFpw1OPyQZ80kv6qLbRx3cDrWbA6i8r0%2BPLR9VBJRaJxq46JEON%2BoS%2BeksAWf7ygMvEXkucGJqpMJHZPW2lrnnbSVXgwi%2BQPuLP7FznaKb%2F71z4ZM48xqPQ7%2Fiag4FO%2F5VbOypLVWqhAeEScb6FSrfNHz9WcQG%2BGj0vcVLSAsXWz%2Bkw&X-Amz-Signature=a3eb51a84e84e42455660d61dcd139d8051ef237a8747e68bb708acad80c425a&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### **Solution  (the easy and unintended way)**

While the extensions with numbers at the end uploaded successful, they were not executed by the server. Uploading and accessing the file as `.phtml` is a different story and executes the script:

![](https://github.com/frank-leitner/portswigger-websecurity-academy/raw/main/08_file_upload_vulnerabilities/Web_shell_upload_via_extension_blacklist_bypass/img/phtml_solution.png)
