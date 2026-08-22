# Web shell upload via extension blacklist bypass

### Goal - 

To solve the lab, upload a basic PHP web shell and use it to exfiltrate the contents of the file `/home/carlos/secret`



### Vulnerability / Concept

This lab demonstrates a vulnerability in the file upload category.

This lab contains a vulnerable image upload function. Certain file extensions are blacklisted, but this defense can be bypassed due to a fundamental flaw in the configuration of this blacklist.

The vulnerability exists because the application fails to properly validate, sanitize, or secure the user-controlled input that reaches a sensitive operation. The specific attack surface and exploitation technique depend on the exact vulnerability type demonstrated in this lab.

### Recon / Initial Analysis

Based on the lab's objective and the PortSwigger solution:

1. Analyze the application's functionality to identify the attack surface
2. Log in and upload an image as your avatar, then go back to your account page.
                    
                    
                        In Burp, go to Proxy &gt; HTTP history and notice that y
3. Use Burp Suite Proxy to intercept and analyze requests
4. Identify the specific vulnerability type by testing user-controlled input
5. Determine the appropriate exploitation technique for this lab

### Analysis/Exploitation -

[Solution  (the easy and unintended way)](https://app.notion.com/p/8133e72ab08a41068a99f5712ad2385b#7008774cb9ca462e9cd076d4095ef174) 

Login as user `wiener`:

In the account settings, I can set both an email address and an avatar image for the user.

upload the PHP script  
`<?php system($_GET['cmd']); ?>`

Trying to upload the php script shows that PHP files are not allowed to upload:

![](./images/8133e72ab08a_001.png)

No file with a PHP extension can be uploaded on the server. Attempts to circumvent this with different capitalization `shell.pHP` or null bytes in the filename `shell.php%00.png` showed no success.

The next step was to try some common alternative extensions for PHP files. The [hacktricks.xyz](https://book.hacktricks.xyz/pentesting-web/file-upload) list a couple of such alternatives for PHP: `phtml, .php, .php3, .php4, .php5`

To bypass this, we can rename the file extension to `.php5`. This extension tells the web server to use PHP version 5.

![](./images/8133e72ab08a_002.png)

We’ve successfully uploaded the web shell!

**Check Can we execute any command?**

![](./images/8133e72ab08a_003.png)

Nope we get plain text of webShell we uploaded.This might happen is because **servers typically won’t execute files unless they have been configured to do so.**

In FireFox extension `Wappalyzer`, it will tell us which web server is using:

![](./images/8133e72ab08a_004.png)

In this case, **the web server is using **`Apache`**.**

{% hint style="info" %}
💡 **In Apache server, before executing PHP files requested by a client, developers might have to add the following directives to their **`/etc/apache2/apache2.conf`** file:**

```text
LoadModule php_module /usr/lib/apache2/modules/libphp.so
AddType application/x-httpd-php .php
```

Many servers also allow developers to create special configuration files within individual directories in order to override or add to one or more of the global settings.

In Apache servers, it will load a directory-specific configuration from a file called `.htaccess` if one is present.

Now, what if I upload a file called `.htaccess` to override the server configuration?

**After poking around, I found this **[**Medium blog**](https://asreshashank.medium.com/execute-php-scripts-into-html-file-by-modifying-htaccess-file-8517ed1e2066)**:**

![](./images/8133e72ab08a_005.png)

{% endhint %}


we can create our own `.htaccess` with the following configuration:

{% hint style="info" %}
`AddType application/x-httpd-php .php5`

**By doing that, we can execute any file that has **`.php5`** extension!**

while uploading intercept the request and **Change the **`Content-Type`** to **`text/plain`**:**

![](./images/8133e72ab08a_006.png)

Or it can be directly uploaded from Burp Repeater, by sending  `POST /my-account/avatar` request that was used to submit the file upload.Make the following changes:

- Change the value of the `filename` parameter to `.htaccess`.
- Change the value of the `Content-Type` header to `text/plain`.
- Replace the contents of the file (your PHP payload) with the following Apache directive: `AddType application/x-httpd-php .php5`
{% endhint %}

{% hint style="info" %}
💡 I noticed that I was able to upload a number of different file extension, possibly even arbitrary ones like `.a2z, .abc` .

If reusing an upload request of `png` or `php` files for the Repeater it is important to set the Content-Type to `text/plain`. Otherwise, the server will return a `500 Internal Server error` when trying to load something later on.

The application is served by an apache server, so uploading a custom .htaccess file maps an arbitrary extension (`.a2z`) to the executable MIME type `application/x-httpd-php`. As the server uses the `mod_php` module, it knows how to handle this already.

{% endhint %}


now we can execute command                                             

![](./images/8133e72ab08a_007.png)

Fetch the carlos secret

![](./images/8133e72ab08a_008.png)

### **Solution  (the easy and unintended way)**

While the extensions with numbers at the end uploaded successful, they were not executed by the server. Uploading and accessing the file as `.phtml` is a different story and executes the script:

![](./images/8133e72ab08a_009.png)

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab contains a vulnerable image upload function. Certain file extensions are blacklisted, but this defense can be bypassed due to a fundamental flaw in the configuration of this blacklist."

### Attack Flow

**Attack Flow:**

```
Attacker Input (payload in request)
        ↓
Application Functionality (processes user input)
        ↓
Server Processing (no validation/sanitization)
        ↓
Injection Point (input reaches sensitive operation)
        ↓
Exploitation (payload executes as intended)
        ↓
Lab Objective Achieved
```

### Real-World Impact

An attacker could achieve remote code execution (RCE) by uploading a web shell, access files on the server, overwrite critical files, or cause denial of service by uploading large files.

### Detection / Testing Methodology

1. Identify file upload functionality (avatars, documents, attachments)
2. Test which file types are accepted (Content-Type, extension)
3. Check if file content is validated (magic bytes)
4. Determine where uploaded files are stored (web-accessible?)
5. Test for path traversal in the filename
6. Test for race conditions in the upload-verify-delete cycle
7. Check if double extensions or null bytes bypass filters

### Remediation

- Validate file content, not just headers (check magic bytes)
- Store uploaded files outside the web root
- Disable script execution in upload directories
- Use random filenames without preserving extensions
- Validate file type using server-side content analysis
- Implement size limits and rate limiting

### Key Takeaways

- This lab demonstrates a file upload vulnerability in a real-world scenario.
- The vulnerability occurs because user input reaches a sensitive operation without proper validation.
- The PortSwigger lab confirms: "This lab contains a vulnerable image upload function. Certain file extensions are blacklisted, but t"
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Validate file content, not just headers (check magic bytes)
