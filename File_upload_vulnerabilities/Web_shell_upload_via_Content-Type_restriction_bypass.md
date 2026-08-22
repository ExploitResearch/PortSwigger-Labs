# Web shell upload via Content-Type restriction bypass

**Lab URL:** https://portswigger.net/web-security/file-upload/lab-file-upload-web-shell-upload-via-content-type-restriction-bypass

### Goal - 

To solve the lab, upload a basic PHP web shell and use it to exfiltrate the contents of the file `/home/carlos/secret`

### Analysis/Exploitation -

Login as user `wiener`:

In the account settings, I can set both an email address and an avatar image for the user.

upload a normal image file

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/File_upload_vulnerabilities/images/c755dab55ab2_001.png)

try to upload the PHP script  
`<?php system($_GET['cmd']); ?>`

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/File_upload_vulnerabilities/images/c755dab55ab2_002.png)

It shows the values for Content-Type that are permitted.

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/File_upload_vulnerabilities/images/c755dab55ab2_003.png)

the `Content-Type` is `application/x-php` and it can be fully-controlled by the attacker.

We can just simply change the `Content-Type` from `application/x-php` to `image/jpeg` or `image/png`

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/File_upload_vulnerabilities/images/c755dab55ab2_004.png)

The file name remained as `webShell.php` so that the server can execute it. Calling the uploaded script with parameter shows the secret data:

the uploaded file stored in `/files/avatar/<filename>`. Let’s trigger the web shell and `cat` the `secret`

via BurpSuite

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/File_upload_vulnerabilities/images/c755dab55ab2_005.png)

via Browser

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/File_upload_vulnerabilities/images/c755dab55ab2_006.png)

via command Curl

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/File_upload_vulnerabilities/images/c755dab55ab2_007.png)

### Why It Works

This lab contains a vulnerable image upload function.
