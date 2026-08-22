# Web shell upload via obfuscated file extension

**Lab URL:** https://portswigger.net/web-security/file-upload/lab-file-upload-web-shell-upload-via-obfuscated-file-extension

### Goal - 

To solve the lab, upload a basic PHP web shell and use it to exfiltrate the contents of the file `/home/carlos/secret`

### Analysis/Exploitation -

Login as user `wiener`:

In the account settings, I can set both an email address and an avatar image for the user.

upload the PHP script  
`<?php system($_GET['cmd']); ?>`

Trying to upload a PHP script as avatar image leads to an error message telling me only some image files are allowed to upload: 

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/File_upload_vulnerabilities/images/b1cb4a9eadd0_001.png)

Send the upload request into Repeater so I can quickly experiment with multiple extension.

To bypass this, we can rename our web shell file to `webshell.php.jpg`:

We successfully uploaded the PHP web shell!

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/File_upload_vulnerabilities/images/b1cb4a9eadd0_002.png)

but the execution of command don’t work

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/File_upload_vulnerabilities/images/b1cb4a9eadd0_003.png)

How about using a null byte(`%00`) and append the `.jpg` extension?By doing that, the null byte will cancel out the `.jpg` extension.

The file get uploaded successfully with name webShell.php

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/File_upload_vulnerabilities/images/b1cb4a9eadd0_004.png)

Some attempts fail to upload or upload as images, including:

- double file extension (`shell.jpg.php`, `shell.php.jpg(it work but script don't execute)`)
- Bypass non recursive filtering (`shell.ph.phpp`)
- trying to split the command (`.php;.jpg`)

However, attempting to terminate the filename early with a null-byte (`shell.php%00.jpg`) proves successful:

now the execution of command is working

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/File_upload_vulnerabilities/images/b1cb4a9eadd0_005.png)

**Let’s **`cat`** the **`secret`** file**

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/File_upload_vulnerabilities/images/b1cb4a9eadd0_006.png)
