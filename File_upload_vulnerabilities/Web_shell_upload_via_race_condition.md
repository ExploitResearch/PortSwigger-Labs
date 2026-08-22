# Web shell upload via race condition

**Lab URL:** https://portswigger.net/web-security/file-upload/lab-file-upload-web-shell-upload-via-race-condition

### Goal -

Exploit a race condition in the file upload process to upload and execute a web shell.

### Exploitation

1. Upload a PHP web shell
2. The application uploads the file, checks it, then deletes it
3. Use Burp Intruder or Turbo Intruder to send many concurrent requests to access the file
4. One of the requests will hit the window between upload and deletion
