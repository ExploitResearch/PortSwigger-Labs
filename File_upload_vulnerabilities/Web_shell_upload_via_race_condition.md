# Web shell upload via race condition

### Goal -

Exploit a race condition in the file upload process to upload and execute a web shell.



### Vulnerability / Concept

This lab demonstrates a vulnerability in the file upload category.

This lab contains a vulnerable image upload function. Although it performs robust validation on any files that are uploaded, it is possible to bypass this validation entirely by exploiting a race condition in the way it processes them.

The vulnerability exists because the application fails to properly validate, sanitize, or secure the user-controlled input that reaches a sensitive operation. The specific attack surface and exploitation technique depend on the exact vulnerability type demonstrated in this lab.

### Recon / Initial Analysis

Based on the lab's objective and the PortSwigger solution:

1. Analyze the application's functionality to identify the attack surface
2. As you can see from the source code above, the uploaded file is moved to an accessible folder, where it is checked for viruses. Malicious files are only removed once the virus check is complete. This 
3. Use Burp Suite Proxy to intercept and analyze requests
4. Identify the specific vulnerability type by testing user-controlled input
5. Determine the appropriate exploitation technique for this lab

### Exploitation

1. Upload a PHP web shell
2. The application uploads the file, checks it, then deletes it
3. Use Burp Intruder or Turbo Intruder to send many concurrent requests to access the file
4. One of the requests will hit the window between upload and deletion

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab contains a vulnerable image upload function. Although it performs robust validation on any files that are uploaded, it is possible to bypass this validation entirely by exploiting a race cond"

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
- The PortSwigger lab confirms: "This lab contains a vulnerable image upload function. Although it performs robust validation on any "
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Validate file content, not just headers (check magic bytes)
