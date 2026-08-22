# burpsuit

## Contents

- [authentication](./authentication/README.md)
- [SQL Injection](./SQL_Injection/README.md)
- [SSRF](./SSRF/README.md)
- [Clickjacking](./Clickjacking/README.md)
- [XSS](./XSS/README.md)
- [CSRF](./CSRF/README.md)
- [Access Control](./Access_Control/README.md)
- [Path/Directory traversal](./PathDirectory_traversal/README.md)
- [File upload vulnerabilities](./File_upload_vulnerabilities/README.md)
- [OS Command Injection ](./OS_Command_Injection/README.md)
- [Business logic vulnerabilities](./Business_logic_vulnerabilities/README.md)
- [Information Disclosure](./Information_Disclosure/README.md)
- [JWT attack](./JWT_attack/README.md)
- [CORS](./CORS/README.md)
- [Race condition](./Race_condition/README.md)
- [API Pentesting](./API_Pentesting.md)
- [XXE](./XXE.md)
- [Extentions](./Extentions.md)

### Identify the Vulnerability (Website Spidering)

Begin by thoroughly examining the web application provided by PortSwigger. Look for input fields, URL parameters, and other user-controllable data points. Use tools like Burp Suite to intercept and analyze requests, identifying potential areas where user input is reflected without proper validation or encoding.

[<span style="color: #BE5B00">**GET vs POST**</span>](/173cb39bf5c94cefb3b333feaaa28d5d#1bc92dd3c4e64b46a12124165a67e920)<span style="color: #BE5B00">**  **</span>A `GET` request contains all parameters in the URL, a `POST` request keeps them in the body of the message.
