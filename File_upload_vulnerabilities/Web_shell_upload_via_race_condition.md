# Web shell upload via race condition

### Goal -

Exploit a race condition in the file upload process to upload and execute a web shell.

### Exploitation

1. Upload a PHP web shell
2. The application uploads the file, checks it, then deletes it
3. Use Burp Intruder or Turbo Intruder to send many concurrent requests to access the file
4. One of the requests will hit the window between upload and deletion

### Why It Works

The exploit succeeds because this lab contains a vulnerable image upload function. although it performs robust validation on any files that are uploaded, it is possible to bypass this validation entirely by exploiting a race cond

The official solution confirms: As you can see from the source code above, the uploaded file is moved to an accessible folder, where it is checked for viruses. Malicious files are on

The root cause is a failure in the application's security architecture specific to this file upload scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- This lab contains vulnerable image upload function, demonstrating how file upload vulnerabilities manifest in real applications.
- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab contains a vulnerable image upload function. Although it performs robust validation on any "
- Validate file content (magic bytes), not just extensions or Content-Type headers.
