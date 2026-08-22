# File path traversal, traversal sequences blocked with absolute path bypass

### Goal - 

Retrieve the contents of the `/etc/passwd` file.



### Vulnerability / Concept

This lab demonstrates a vulnerability in the file path traversal category.

This lab contains a path traversal vulnerability in the display of product images.

The vulnerability exists because the application fails to properly validate, sanitize, or secure the user-controlled input that reaches a sensitive operation. The specific attack surface and exploitation technique depend on the exact vulnerability type demonstrated in this lab.

### Recon / Initial Analysis

Based on the lab's objective and the PortSwigger solution:

1. Analyze the application's functionality to identify the attack surface
2. Use Burp Suite to intercept and modify a request that fetches a product image.
                    
                    
                        
                            Modify the filename parame
3. Use Burp Suite Proxy to intercept and analyze requests
4. Identify the specific vulnerability type by testing user-controlled input
5. Determine the appropriate exploitation technique for this lab

### Analysis/Exploitation 

open any product or open any image in new tab

![](./images/37ac64c35968_001.png)

apply above filter to see image request and sent it to repeater

![](./images/37ac64c35968_002.png)

This time however, the application blocks traversal sequences,requesting `../../../etc/passwd` does not lead to any file,If the webserver's default working directory is assumed when no path is explicitly given.

The application prepends this default working directory to the requested filename before trying to access the file (e.g. something like `'/var/html/www/' + $_REQUEST["filename"]`, the hardcoded first part could be interpreted as 'default working directory').Providing an absolute path could be the solution to exploit the path traversal vulnerability.

To bypass this, we can just provide the absolute path of the `/etc/passwd`:

![](./images/37ac64c35968_003.png)

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab contains a path traversal vulnerability in the display of product images."

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

An attacker could read arbitrary files on the server (/etc/passwd, configuration files, source code, credentials), access sensitive application data, or cause denial of service by reading large files.

### Detection / Testing Methodology

1. Identify parameters that accept file paths or filenames (image paths, document paths, template names)
2. Test with basic traversal sequences (../../../etc/passwd)
3. Test absolute paths (/etc/passwd, C:\\Windows\\win.ini)
4. Test encoding bypasses (URL encoding, double encoding, Unicode)
5. Test null byte injection (file.txt%00.jpg)
6. Check if the application strips traversal sequences (and if non-recursive stripping can be bypassed)

### Remediation

- Validate that the supplied filename is within the expected directory (canonicalize and check)
- Do not accept user-supplied file paths — use indirect references (IDs mapped to filenames)
- Strip or reject path traversal sequences (../, ..\, %2e%2e%2f, etc.)
- Use allowlists for expected filenames
- Run the application with least privilege (no access to system files)
- Implement chroot or containerized environments

### Key Takeaways

- This lab demonstrates a file path traversal vulnerability in a real-world scenario.
- The vulnerability occurs because user input reaches a sensitive operation without proper validation.
- The PortSwigger lab confirms: "This lab contains a path traversal vulnerability in the display of product images."
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Validate that the supplied filename is within the expected directory (canonicalize and check)
