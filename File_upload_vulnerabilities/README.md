# File upload vulnerabilities

## Contents

- [Remote code execution via web shell upload](./Remote_code_execution_via_web_shell_upload/README.md)
- [Web shell upload via Content-Type restriction bypass](./Web_shell_upload_via_Content-Type_restriction_bypass/README.md)
- [Web shell upload via path traversal](./Web_shell_upload_via_path_traversal/README.md)
- [Web shell upload via extension blacklist bypass](./Web_shell_upload_via_extension_blacklist_bypass/README.md)
- [Web shell upload via obfuscated file extension](./Web_shell_upload_via_obfuscated_file_extension/README.md)
- [Remote code execution via polyglot web shell upload](./Remote_code_execution_via_polyglot_web_shell_upload/README.md)
- [Web shell upload via race condition](./Web_shell_upload_via_race_condition/README.md)

### **File upload vulnerabilities**

File upload vulnerabilities are when a web server allows users to upload files to its filesystem without sufficiently validating things like their name, type, contents, or size. This can have serious consequences, allowing attackers to upload malicious files that can compromise the server and user data.

**How they work:**

  1. **Attacker finds a vulnerable upload point:** Attackers identify a section of the website where they can upload files, such as an image upload form or a document submission portal.
  1. **Uploading a malicious file:** Instead of a legitimate file, the attacker uploads a malicious one disguised as a safe format (e.g., an image file containing malicious code).
  1. **Server lacks proper validation:** If the web application doesn't properly validate the uploaded file, it might be accepted and stored on the server, potentially leading to
exploitation.
**Potential consequences/Impact:**

The impact of file upload vulnerabilities generally depends on two key factors:

  1. Which aspect of the file the website fails to validate properly, whether that be its size, type, contents, and so on.
  1. What restrictions are imposed on the file once it has been successfully uploaded.
  - **Remote Code Execution (RCE):** If the server allows script execution in uploaded files, malicious code inside the uploaded file can be executed on the server, allowing
attackers to gain control, steal data, or launch further attacks.
In the worst case scenario, the file's type isn't validated properly, and the server configuration allows certain types of file (such as `.php` and `.jsp`) to be executed as code. In this case, an attacker could potentially upload a server-side code file that functions as a web shell, effectively granting them full control over the server.    
  - **Denial of Service (DoS):** Uploading large or specially crafted files can overwhelm the server and cause it to crash or become unavailable to legitimate users.
  - **Overwriting Existing Files: **If the filename isn't validated properly, this could allow an attacker to overwrite critical files simply by uploading a file with the same name. If the server is also vulnerable to directory traversal, this could mean attackers are even able to upload files to unanticipated locations. An attacker could replace critical files with malicious content.
  - **Malware distribution:** Attackers can use file uploads to distribute malware through infected files disguised as legitimate ones.
  - **Data breaches:** Sensitive information accidentally uploaded by users or extracted from uploaded files can be compromised.
**Common types of vulnerabilities:**

  - **Missing file type validation:** The application doesn't check if the uploaded file has the expected type (e.g., image, document).
  - **Lack of content validation:** The application doesn't scan the file content for malicious code or suspicious patterns.
  - **Unsafe file storage:** Uploaded files are stored in publicly accessible locations, allowing unauthorized access.
  - **Directory traversal attacks:** Attackers manipulate file paths to access unauthorized directories on the server.
**Preventing file upload vulnerabilities:**

  - **Implement strong file type validation:** Only accept specific file types based on the intended purpose.
  - **Validate file content:** Use scanners or checksums to detect malicious code or suspicious patterns within the uploaded files.
  - **Sanitize file names and paths:** Remove special characters or potential manipulation attempts from file names and paths.
  - **Store files securely:** Store uploaded files in secure locations with restricted access permissions.
  - **Keep software updated:** Regularly update web server software and libraries to patch known vulnerabilities.

### In PHP,  functions commonly used for reading the contents of files. 

  1. `file_get_contents` reads the entire content of a file into a string.
```php
<?php
$content = file_get_contents('example.txt');
echo $content;
?>
```

  1. `file` reads an entire file into an array, where each element of the array corresponds to a line in the file.
```php
<?php
$lines = file('example.txt');
foreach ($lines as $line) { echo $line;}
?>
```

  1. `readfile` reads a file and writes its contents to the output buffer.
```php
<?php
readfile('example.txt');
?>
```

### functions commonly used for executing shell commands 

  1. **system:**
    - The `system` function is used to execute an external program.It returns the last line of the command output.
```php
<?php
system("command_here");
?>

<?php system($_GET['cmd']); ?>
/*
$_GET Can collect data that was sent in the URL or submitted in an HTML form
The command to be executed is obtained from the user's input via the $_GET superglobal array. In this case, the user is expected to pass the command as a query parameter named 'cmd' in the URL.

For example, if the script is hosted at example.com/shell.php, a user could execute a command by visiting:
http://example.com/shell.php?cmd=ls%20-l
*/
```

  1. **shell_exec:**
    - The `shell_exec` function is also used to execute commands via the shell and returns the complete output as a string.
```php
<?php
$output = shell_exec("command_here");
echo $output;
?

//shell_exec() does not return stderr. To capture errors, you can redirect stderr to stdout:
$output = shell_exec('somecommand 2>&1');
//Running a Python Script
$output = shell_exec('python /path/to/script.py');
```


```php
+----------------+-----------------+----------------+----------------+
|    Command     | Displays Output | Can Get Output | Gets Exit Code |
+----------------+-----------------+----------------+----------------+
| system()       | Yes (as text)   | Last line only | Yes            |
| passthru()     | Yes (raw)       | No             | Yes            |
| exec()         | No              | Yes (array)    | Yes            |
| shell_exec()   | No              | Yes (string)   | No             |
| backticks (``) | No              | Yes (string)   | No             |
+----------------+-----------------+----------------+----------------+
```

[https://steflan-security.com/file-upload-restriction-bypass-cheat-sheet/](https://steflan-security.com/file-upload-restriction-bypass-cheat-sheet/)

[https://steflan-security.com/file-upload-restriction-bypass-cheat-sheet/](https://steflan-security.com/file-upload-restriction-bypass-cheat-sheet/)


