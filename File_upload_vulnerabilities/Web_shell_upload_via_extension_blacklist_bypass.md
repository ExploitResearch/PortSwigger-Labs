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

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/6255eea3-0949-47c4-84bd-c5ea9289511b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4665EYCUTJX%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210418Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDqvJURl6h5Y%2B40p3Xc6cXUDHdR9j3rCgpMvYZyJknPLQIgNSYhEW7zgrAA1Ia7Drivik2tk4mHU9Q%2BMLJEe0pqXrcqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDC574kjWR27oauLNeSrcAzxKqcxjbSV7MYnuM6OfQMoKyOuTFOkAnbC%2B9imICcKLAcg7qDWsm70qUTfeKZsDaX0SUoYKEPRKfrUMR9wAHPPXxMZCPJlDKhu9lxxURM2S9798YeitN3%2BiLw6UDCW6%2FSZqrt7fGLn3%2BWCEnjXBByeyZ2FCzLE03EoZArUaMvcydkVXa7BxoUPfSQzlV%2BLY1%2FQ3bxpqQyV8GSrh6nNhhB2ncGCKYbxuVTdGSxROceWm7pgmMu%2BOCTR53cj65sPPvKTQ3fNcYqdpGZ1U%2B3EmznqLMfe6CwEqc%2BYZ36BoP0YjIDPBug47BIcS4uJNtsKXGDO8aTI698zrLc7I0s02eoWF6CitNxkQWEMc3QiLPUKPEZrehZYa7awA5T%2BGeP1ZtyFeQ9C%2FrlzreVXvSVmDDPTmtl2vVnQphiaK3xUoxPwj9QU60p1Er4RXyxkqTs5qh8TwiPHvnlE2gFrDyIkClE6HnPTGgCoTdGDVSIT93rnvGvCYCb1DLqtEa8Smou5dmewIh9Q39eVuLRD2z4g4EbY%2B7%2FPZI7V7Rv3qicrMm%2BHT1o6uJhV1yRb5uFIB9cxTUSHRBb0e5OR%2F4mc%2FdeR1PbjazOYTrdGIkIRGYbYJhdQU%2B7Zg8Mt%2F7BMV5ZhPMO%2FFotQGOqUBmeOQLjyZe6TkgK%2FsVCiVbYgq6MODehze9H%2B9kPd466%2Fq9Ak4O18A1680i8dBI%2FWExRUZ5laERX9ZqRvVfh94x0vgb6T9d5cjRLUEr9kMFFioJhSm%2Be9Y4VigqgRaYcWYDWY6vPM2k29FQkmLrWlZSeaJwNC%2BEiA%2FBN1bh3L4uOdRv182yt9E9%2B6Dicxfz4Vcw0Tncykjt2kLKA8Y6m8luE6yZlQK&X-Amz-Signature=5c6e7c618c0730905cf76a2f52166923182f3b49a015a5aa76a46fe55cb42737&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

No file with a PHP extension can be uploaded on the server. Attempts to circumvent this with different capitalization `shell.pHP` or null bytes in the filename `shell.php%00.png` showed no success.

The next step was to try some common alternative extensions for PHP files. The [hacktricks.xyz](https://book.hacktricks.xyz/pentesting-web/file-upload) list a couple of such alternatives for PHP: `phtml, .php, .php3, .php4, .php5`

To bypass this, we can rename the file extension to `.php5`. This extension tells the web server to use PHP version 5.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/7db30d74-5e6c-4e48-a2c6-385808857d7d/2024-03-01_07-57.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4665EYCUTJX%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210418Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDqvJURl6h5Y%2B40p3Xc6cXUDHdR9j3rCgpMvYZyJknPLQIgNSYhEW7zgrAA1Ia7Drivik2tk4mHU9Q%2BMLJEe0pqXrcqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDC574kjWR27oauLNeSrcAzxKqcxjbSV7MYnuM6OfQMoKyOuTFOkAnbC%2B9imICcKLAcg7qDWsm70qUTfeKZsDaX0SUoYKEPRKfrUMR9wAHPPXxMZCPJlDKhu9lxxURM2S9798YeitN3%2BiLw6UDCW6%2FSZqrt7fGLn3%2BWCEnjXBByeyZ2FCzLE03EoZArUaMvcydkVXa7BxoUPfSQzlV%2BLY1%2FQ3bxpqQyV8GSrh6nNhhB2ncGCKYbxuVTdGSxROceWm7pgmMu%2BOCTR53cj65sPPvKTQ3fNcYqdpGZ1U%2B3EmznqLMfe6CwEqc%2BYZ36BoP0YjIDPBug47BIcS4uJNtsKXGDO8aTI698zrLc7I0s02eoWF6CitNxkQWEMc3QiLPUKPEZrehZYa7awA5T%2BGeP1ZtyFeQ9C%2FrlzreVXvSVmDDPTmtl2vVnQphiaK3xUoxPwj9QU60p1Er4RXyxkqTs5qh8TwiPHvnlE2gFrDyIkClE6HnPTGgCoTdGDVSIT93rnvGvCYCb1DLqtEa8Smou5dmewIh9Q39eVuLRD2z4g4EbY%2B7%2FPZI7V7Rv3qicrMm%2BHT1o6uJhV1yRb5uFIB9cxTUSHRBb0e5OR%2F4mc%2FdeR1PbjazOYTrdGIkIRGYbYJhdQU%2B7Zg8Mt%2F7BMV5ZhPMO%2FFotQGOqUBmeOQLjyZe6TkgK%2FsVCiVbYgq6MODehze9H%2B9kPd466%2Fq9Ak4O18A1680i8dBI%2FWExRUZ5laERX9ZqRvVfh94x0vgb6T9d5cjRLUEr9kMFFioJhSm%2Be9Y4VigqgRaYcWYDWY6vPM2k29FQkmLrWlZSeaJwNC%2BEiA%2FBN1bh3L4uOdRv182yt9E9%2B6Dicxfz4Vcw0Tncykjt2kLKA8Y6m8luE6yZlQK&X-Amz-Signature=1d684f1772f0d89b899cee4b73bff311357dd25a48bd9974235ed3d2d31e8474&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

We’ve successfully uploaded the web shell!

**Check Can we execute any command?**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/9d20721b-088c-465c-855d-c047a2298ef0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4665EYCUTJX%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210418Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDqvJURl6h5Y%2B40p3Xc6cXUDHdR9j3rCgpMvYZyJknPLQIgNSYhEW7zgrAA1Ia7Drivik2tk4mHU9Q%2BMLJEe0pqXrcqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDC574kjWR27oauLNeSrcAzxKqcxjbSV7MYnuM6OfQMoKyOuTFOkAnbC%2B9imICcKLAcg7qDWsm70qUTfeKZsDaX0SUoYKEPRKfrUMR9wAHPPXxMZCPJlDKhu9lxxURM2S9798YeitN3%2BiLw6UDCW6%2FSZqrt7fGLn3%2BWCEnjXBByeyZ2FCzLE03EoZArUaMvcydkVXa7BxoUPfSQzlV%2BLY1%2FQ3bxpqQyV8GSrh6nNhhB2ncGCKYbxuVTdGSxROceWm7pgmMu%2BOCTR53cj65sPPvKTQ3fNcYqdpGZ1U%2B3EmznqLMfe6CwEqc%2BYZ36BoP0YjIDPBug47BIcS4uJNtsKXGDO8aTI698zrLc7I0s02eoWF6CitNxkQWEMc3QiLPUKPEZrehZYa7awA5T%2BGeP1ZtyFeQ9C%2FrlzreVXvSVmDDPTmtl2vVnQphiaK3xUoxPwj9QU60p1Er4RXyxkqTs5qh8TwiPHvnlE2gFrDyIkClE6HnPTGgCoTdGDVSIT93rnvGvCYCb1DLqtEa8Smou5dmewIh9Q39eVuLRD2z4g4EbY%2B7%2FPZI7V7Rv3qicrMm%2BHT1o6uJhV1yRb5uFIB9cxTUSHRBb0e5OR%2F4mc%2FdeR1PbjazOYTrdGIkIRGYbYJhdQU%2B7Zg8Mt%2F7BMV5ZhPMO%2FFotQGOqUBmeOQLjyZe6TkgK%2FsVCiVbYgq6MODehze9H%2B9kPd466%2Fq9Ak4O18A1680i8dBI%2FWExRUZ5laERX9ZqRvVfh94x0vgb6T9d5cjRLUEr9kMFFioJhSm%2Be9Y4VigqgRaYcWYDWY6vPM2k29FQkmLrWlZSeaJwNC%2BEiA%2FBN1bh3L4uOdRv182yt9E9%2B6Dicxfz4Vcw0Tncykjt2kLKA8Y6m8luE6yZlQK&X-Amz-Signature=3eb03b7977dcd889ad8a5bc5f5a17610a7acc2f78ee947950c5b6ba9c3b71f4e&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/7da44160-911a-4b1a-9d8a-08b467fa0cc0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4665EYCUTJX%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210418Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDqvJURl6h5Y%2B40p3Xc6cXUDHdR9j3rCgpMvYZyJknPLQIgNSYhEW7zgrAA1Ia7Drivik2tk4mHU9Q%2BMLJEe0pqXrcqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDC574kjWR27oauLNeSrcAzxKqcxjbSV7MYnuM6OfQMoKyOuTFOkAnbC%2B9imICcKLAcg7qDWsm70qUTfeKZsDaX0SUoYKEPRKfrUMR9wAHPPXxMZCPJlDKhu9lxxURM2S9798YeitN3%2BiLw6UDCW6%2FSZqrt7fGLn3%2BWCEnjXBByeyZ2FCzLE03EoZArUaMvcydkVXa7BxoUPfSQzlV%2BLY1%2FQ3bxpqQyV8GSrh6nNhhB2ncGCKYbxuVTdGSxROceWm7pgmMu%2BOCTR53cj65sPPvKTQ3fNcYqdpGZ1U%2B3EmznqLMfe6CwEqc%2BYZ36BoP0YjIDPBug47BIcS4uJNtsKXGDO8aTI698zrLc7I0s02eoWF6CitNxkQWEMc3QiLPUKPEZrehZYa7awA5T%2BGeP1ZtyFeQ9C%2FrlzreVXvSVmDDPTmtl2vVnQphiaK3xUoxPwj9QU60p1Er4RXyxkqTs5qh8TwiPHvnlE2gFrDyIkClE6HnPTGgCoTdGDVSIT93rnvGvCYCb1DLqtEa8Smou5dmewIh9Q39eVuLRD2z4g4EbY%2B7%2FPZI7V7Rv3qicrMm%2BHT1o6uJhV1yRb5uFIB9cxTUSHRBb0e5OR%2F4mc%2FdeR1PbjazOYTrdGIkIRGYbYJhdQU%2B7Zg8Mt%2F7BMV5ZhPMO%2FFotQGOqUBmeOQLjyZe6TkgK%2FsVCiVbYgq6MODehze9H%2B9kPd466%2Fq9Ak4O18A1680i8dBI%2FWExRUZ5laERX9ZqRvVfh94x0vgb6T9d5cjRLUEr9kMFFioJhSm%2Be9Y4VigqgRaYcWYDWY6vPM2k29FQkmLrWlZSeaJwNC%2BEiA%2FBN1bh3L4uOdRv182yt9E9%2B6Dicxfz4Vcw0Tncykjt2kLKA8Y6m8luE6yZlQK&X-Amz-Signature=10563256cef4320c86cd312ca658e72e9f1fc7ba3b88367a6d73b77699e36fe9&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Or it can be directly uploaded from Burp Repeater, by sending  `POST /my-account/avatar` request that was used to submit the file upload.Make the following changes:

- Change the value of the `filename` parameter to `.htaccess`.
- Change the value of the `Content-Type` header to `text/plain`.
- Replace the contents of the file (your PHP payload) with the following Apache directive: `AddType application/x-httpd-php .php5`
> 💡 I noticed that I was able to upload a number of different file extension, possibly even arbitrary ones like `.a2z, .abc` .

If reusing an upload request of `png` or `php` files for the Repeater it is important to set the Content-Type to `text/plain`. Otherwise, the server will return a `500 Internal Server error` when trying to load something later on.

The application is served by an apache server, so uploading a custom .htaccess file maps an arbitrary extension (`.a2z`) to the executable MIME type `application/x-httpd-php`. As the server uses the `mod_php` module, it knows how to handle this already.

now we can execute command                                             

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/d35ddc09-b43d-40d8-a145-c24c4978f3d5/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4665EYCUTJX%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210418Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDqvJURl6h5Y%2B40p3Xc6cXUDHdR9j3rCgpMvYZyJknPLQIgNSYhEW7zgrAA1Ia7Drivik2tk4mHU9Q%2BMLJEe0pqXrcqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDC574kjWR27oauLNeSrcAzxKqcxjbSV7MYnuM6OfQMoKyOuTFOkAnbC%2B9imICcKLAcg7qDWsm70qUTfeKZsDaX0SUoYKEPRKfrUMR9wAHPPXxMZCPJlDKhu9lxxURM2S9798YeitN3%2BiLw6UDCW6%2FSZqrt7fGLn3%2BWCEnjXBByeyZ2FCzLE03EoZArUaMvcydkVXa7BxoUPfSQzlV%2BLY1%2FQ3bxpqQyV8GSrh6nNhhB2ncGCKYbxuVTdGSxROceWm7pgmMu%2BOCTR53cj65sPPvKTQ3fNcYqdpGZ1U%2B3EmznqLMfe6CwEqc%2BYZ36BoP0YjIDPBug47BIcS4uJNtsKXGDO8aTI698zrLc7I0s02eoWF6CitNxkQWEMc3QiLPUKPEZrehZYa7awA5T%2BGeP1ZtyFeQ9C%2FrlzreVXvSVmDDPTmtl2vVnQphiaK3xUoxPwj9QU60p1Er4RXyxkqTs5qh8TwiPHvnlE2gFrDyIkClE6HnPTGgCoTdGDVSIT93rnvGvCYCb1DLqtEa8Smou5dmewIh9Q39eVuLRD2z4g4EbY%2B7%2FPZI7V7Rv3qicrMm%2BHT1o6uJhV1yRb5uFIB9cxTUSHRBb0e5OR%2F4mc%2FdeR1PbjazOYTrdGIkIRGYbYJhdQU%2B7Zg8Mt%2F7BMV5ZhPMO%2FFotQGOqUBmeOQLjyZe6TkgK%2FsVCiVbYgq6MODehze9H%2B9kPd466%2Fq9Ak4O18A1680i8dBI%2FWExRUZ5laERX9ZqRvVfh94x0vgb6T9d5cjRLUEr9kMFFioJhSm%2Be9Y4VigqgRaYcWYDWY6vPM2k29FQkmLrWlZSeaJwNC%2BEiA%2FBN1bh3L4uOdRv182yt9E9%2B6Dicxfz4Vcw0Tncykjt2kLKA8Y6m8luE6yZlQK&X-Amz-Signature=438f064fc785a3493b73a68ea6c4dfc9daf058304c61ffa15d469ad8c9f5a31c&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Fetch the carlos secret

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/73346238-3276-4754-9349-8bd022136e88/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4665EYCUTJX%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210418Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQDqvJURl6h5Y%2B40p3Xc6cXUDHdR9j3rCgpMvYZyJknPLQIgNSYhEW7zgrAA1Ia7Drivik2tk4mHU9Q%2BMLJEe0pqXrcqiAQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDC574kjWR27oauLNeSrcAzxKqcxjbSV7MYnuM6OfQMoKyOuTFOkAnbC%2B9imICcKLAcg7qDWsm70qUTfeKZsDaX0SUoYKEPRKfrUMR9wAHPPXxMZCPJlDKhu9lxxURM2S9798YeitN3%2BiLw6UDCW6%2FSZqrt7fGLn3%2BWCEnjXBByeyZ2FCzLE03EoZArUaMvcydkVXa7BxoUPfSQzlV%2BLY1%2FQ3bxpqQyV8GSrh6nNhhB2ncGCKYbxuVTdGSxROceWm7pgmMu%2BOCTR53cj65sPPvKTQ3fNcYqdpGZ1U%2B3EmznqLMfe6CwEqc%2BYZ36BoP0YjIDPBug47BIcS4uJNtsKXGDO8aTI698zrLc7I0s02eoWF6CitNxkQWEMc3QiLPUKPEZrehZYa7awA5T%2BGeP1ZtyFeQ9C%2FrlzreVXvSVmDDPTmtl2vVnQphiaK3xUoxPwj9QU60p1Er4RXyxkqTs5qh8TwiPHvnlE2gFrDyIkClE6HnPTGgCoTdGDVSIT93rnvGvCYCb1DLqtEa8Smou5dmewIh9Q39eVuLRD2z4g4EbY%2B7%2FPZI7V7Rv3qicrMm%2BHT1o6uJhV1yRb5uFIB9cxTUSHRBb0e5OR%2F4mc%2FdeR1PbjazOYTrdGIkIRGYbYJhdQU%2B7Zg8Mt%2F7BMV5ZhPMO%2FFotQGOqUBmeOQLjyZe6TkgK%2FsVCiVbYgq6MODehze9H%2B9kPd466%2Fq9Ak4O18A1680i8dBI%2FWExRUZ5laERX9ZqRvVfh94x0vgb6T9d5cjRLUEr9kMFFioJhSm%2Be9Y4VigqgRaYcWYDWY6vPM2k29FQkmLrWlZSeaJwNC%2BEiA%2FBN1bh3L4uOdRv182yt9E9%2B6Dicxfz4Vcw0Tncykjt2kLKA8Y6m8luE6yZlQK&X-Amz-Signature=35b4f906b86a75ad961dbe952043792619dcff0e7984a2a911ef1ea84e85d1ce&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)


### **Solution  (the easy and unintended way)**

While the extensions with numbers at the end uploaded successful, they were not executed by the server. Uploading and accessing the file as `.phtml` is a different story and executes the script:

![](https://github.com/frank-leitner/portswigger-websecurity-academy/raw/main/08_file_upload_vulnerabilities/Web_shell_upload_via_extension_blacklist_bypass/img/phtml_solution.png)
