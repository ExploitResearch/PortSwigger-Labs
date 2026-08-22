# Web shell upload via race condition

### Goal -

Exploit a race condition in the file upload process to upload and execute a web shell.

### Vulnerability / Concept

The application checks the file after upload but briefly serves it before deleting it. By sending many requests simultaneously, the attacker can access the file during the window between upload and deletion.

### Exploitation

1. Upload a PHP web shell
2. The application uploads the file, checks it, then deletes it
3. Use Burp Intruder or Turbo Intruder to send many concurrent requests to access the file
4. One of the requests will hit the window between upload and deletion

### Why It Works

The application has a TOCTOU (Time-of-Check-Time-of-Use) vulnerability. The file is briefly accessible on the server between the upload and the validation/deletion. By racing many requests, the attacker can access the file during this window.

### Key Takeaways

- Validate files BEFORE writing them to the web-accessible directory
- Use a temporary directory for validation
- Delete invalid files from a non-web-accessible location
- Implement atomic file operations
