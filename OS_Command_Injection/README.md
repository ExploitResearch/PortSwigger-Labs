# OS Command Injection 

## Contents

- [OS command injection, simple case](./OS_command_injection,_simple_case/README.md)
- [Blind OS command injection with time delays](./Blind_OS_command_injection_with_time_delays/README.md)
- [Blind OS command injection with output redirection](./Blind_OS_command_injection_with_output_redirection/README.md)
- [Blind OS command injection with out-of-band interaction](./Blind_OS_command_injection_with_out-of-band_interaction/README.md)
- [Blind OS command injection with out-of-band data exfiltration](./Blind_OS_command_injection_with_out-of-band_data_exfiltration/README.md)

OS command injection is also known as shell injection. It allows an attacker to execute operating system (OS) commands on the server that is running an application, and typically fully compromise the application and its data. Often, an attacker can leverage an OS command injection vulnerability to compromise other parts of the hosting infrastructure, and exploit trust relationships to pivot the attack to other systems within the organization.

The better question is what is command injection? well a command injection is way by which an attacker can execute arbitrary commands because of improper data processing or some vulnerability. A command injection can lead to various attacks like JavaScript code injection, HTML Template injection, etc. One such attack is OS Command Injection. In which attacker can execute arbitrary OS commands on target Operating System or server where application is deployed.

### Types of Command Injection

  1. **In-band Command Injection**
Consists of an attacker executing commands on the host operating system via a vulnerable application and receiving the response of the command in the application.
  1. **Blind/out-of-band Command Injection**
Consists of an attacker executing commands on the host operating system via a vulnerable application that does not return the output from the command within its HTTP response.
| Purpose of command | Linux | Windows |
| Name of current user | `whoami` | `whoami` |
| Operating system | `uname -a` | `ver` |
| Network configuration | `ifconfig` | `ipconfig /all` |
| Network connections | `netstat -an` | `netstat -an` |
| Running processes | `ps -ef` | `tasklist` |
### Impact of Command Injection Attacks

  1. Unauthorized access to the application and host operating system.
• Confidentiality – Command injection can be used to view sensitive information.
• Integrity – Command injection can be used to alter content in the application.
• Availability – Command injection can be used to delete content in the application.
  1. Remote code execution on the operating system
### Finding Command Injection Vulnerabilities

**Black-Box Testing**

  1. Map the application.
    - Identify all instances where the web application appears to be interacting with the underlying operating system.
  1. Fuzz the application.
    - Shell metacharacters: **&, &&, |, ||, ;, \n, `, $().**
  1. For in-band command injection, analyze the response of the application to determine if it's vulnerable.
  1. For blind command injection, you need to get creative.
    - Trigger a time delay using the ping or sleep command.
    - Output the response of the command in the web root and retrieve the file directly using a browser.
    - Open an out-of-band channel back to a server you control.
**White-Box Testing**

  1. Perform a combination of black box and white-box testing.
  1. Map all input vectors in the application.
  1. Review source code to determine if any of the input vectors are added as parameters to functions that execute system commands.
  1. Once a vulnerability is identified, test it to confirm that it is exploitable.
### HOW TO EXPLOIT COMMAND INJECTION

### **Exploiting In-band Command Injection**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/24e41551-1b5a-441c-af75-c4e724e66e54/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466RVVSERUY%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210424Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIBKUQc4%2FQ6H8Ex%2B%2F1aQzHyIHHhE9MS%2FipOQkE5P3szHPAiBRvauCMYHqukpp%2Bzrl3LU6O%2FBc6Z5WRtYz%2F8oDKJ8G%2FiqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMWjnnEOyYT%2B7LQfazKtwD3x1FOUs0ZYA%2F%2FbRcxxKEwu5C9Yi12zxkj3nhkxmnmaO2iQXSfHebSl91kfE9LU4W6v2K9HJhQAkEEzOzAQEQsPx4TnOhEWx%2FNIOpiCG9OCqfmE40oJ8BVTJGa2BpTsO7IVcVshbCneafL3hCPmoRrQBKA9hzT9y4ZJag2RPx%2BrJrH9%2BQbqoMGMbCqBVRK37j4JhgxNSi%2B82NTnRzJFIqawQVkA%2FpRWQhikRCs5aV6mBF9TlcM072YnLxg5otTApJWNnOx8op7fHIljDaQ3q4u81Q3nB6G5Rtu%2FEAlsIrTq0Gxb2WhOkvXfnf5%2B1OZcINxul0ts3bn6ZbWeUIKpp%2B4nc0IOGYNRfRPzrptszoqidDvHVLU85eUZU%2Fym%2F3CvmZs8xG9rzLI2Kw8wbO5m8LqfKcs9DOr2btNVU2Vu9hUJMOYlVLZaqJH9gbz71sf38TM7E1uMOjbscuR9K%2BzkclOCgI1XfoPdMeS5Z%2F345HHXjZlEamepUVEuhJUNMrZ1EWGxQrYm%2BC96bU2MDNKRInKyDoJOMd3Gv6gd%2Fma7fZf%2BsoBkrRCmRO3vOyr%2FY%2BNQFR4NxzqCinuTqoxfTvr7kpn6eKADS1fMf2FJLpby7t3Ng2t3TPJQ0shLnSlpkw8cWi1AY6pgF%2Fyte3w2ziluKSFV2rEjg4B3Rg%2FI%2FaOadm6QrGJ8jbZXBMdVI9BtP9Q98OpAuxw0PpAxr9ARoN6eNEl07fp7OENu6caERQoAaxrK3YH5rlFLiI6PGKNFBzFwfYxptGQBvGvIz1MqnKNpvKGO%2BD3Il2fxlVggqQIUTSlQAvPSh8eVUrV9eRRCixwl0jwCpgCCKfN4f%2BY4xg7hGFl9Gyyxhe2gWXFAT3&X-Amz-Signature=3c71eeba612970ec6ddc5d2d8477da09242857125de6c18480a84a1a00469851&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### **Exploiting Blind Command Injection**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/0db89c61-c15c-45fa-9405-f9e6b2e4fc22/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466RVVSERUY%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210424Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIBKUQc4%2FQ6H8Ex%2B%2F1aQzHyIHHhE9MS%2FipOQkE5P3szHPAiBRvauCMYHqukpp%2Bzrl3LU6O%2FBc6Z5WRtYz%2F8oDKJ8G%2FiqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMWjnnEOyYT%2B7LQfazKtwD3x1FOUs0ZYA%2F%2FbRcxxKEwu5C9Yi12zxkj3nhkxmnmaO2iQXSfHebSl91kfE9LU4W6v2K9HJhQAkEEzOzAQEQsPx4TnOhEWx%2FNIOpiCG9OCqfmE40oJ8BVTJGa2BpTsO7IVcVshbCneafL3hCPmoRrQBKA9hzT9y4ZJag2RPx%2BrJrH9%2BQbqoMGMbCqBVRK37j4JhgxNSi%2B82NTnRzJFIqawQVkA%2FpRWQhikRCs5aV6mBF9TlcM072YnLxg5otTApJWNnOx8op7fHIljDaQ3q4u81Q3nB6G5Rtu%2FEAlsIrTq0Gxb2WhOkvXfnf5%2B1OZcINxul0ts3bn6ZbWeUIKpp%2B4nc0IOGYNRfRPzrptszoqidDvHVLU85eUZU%2Fym%2F3CvmZs8xG9rzLI2Kw8wbO5m8LqfKcs9DOr2btNVU2Vu9hUJMOYlVLZaqJH9gbz71sf38TM7E1uMOjbscuR9K%2BzkclOCgI1XfoPdMeS5Z%2F345HHXjZlEamepUVEuhJUNMrZ1EWGxQrYm%2BC96bU2MDNKRInKyDoJOMd3Gv6gd%2Fma7fZf%2BsoBkrRCmRO3vOyr%2FY%2BNQFR4NxzqCinuTqoxfTvr7kpn6eKADS1fMf2FJLpby7t3Ng2t3TPJQ0shLnSlpkw8cWi1AY6pgF%2Fyte3w2ziluKSFV2rEjg4B3Rg%2FI%2FaOadm6QrGJ8jbZXBMdVI9BtP9Q98OpAuxw0PpAxr9ARoN6eNEl07fp7OENu6caERQoAaxrK3YH5rlFLiI6PGKNFBzFwfYxptGQBvGvIz1MqnKNpvKGO%2BD3Il2fxlVggqQIUTSlQAvPSh8eVUrV9eRRCixwl0jwCpgCCKfN4f%2BY4xg7hGFl9Gyyxhe2gWXFAT3&X-Amz-Signature=2613802b77b2dc1209b997a7edfd2817d6a9909c13faf5b8943da33232d313a1&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### Ways of injecting OS commands

You can use a number of shell metacharacters to perform OS command injection attacks.

A number of characters function as command separators, allowing commands to be chained together. 

The following command separators work on both Windows and Unix-based systems:

  - `&`
  - `&&`
  - `|`
  - `||`
The following command separators work only on Unix-based systems:

  - `;`
  - Newline (`0x0a` or `\n`)
On Unix-based systems, you can also use backticks or the dollar character to perform inline execution of an injected command within the original command:

  - ``` injected command ```
  - `$(` injected command `)`
Sometimes, the input that you control appears within quotation marks in the original command. In this situation, you need to terminate the quoted context (using `"` or `'`) before using suitable shell metacharacters to inject a new command.

### Preventing Command Injection Vulnerabilities

  1. The most effective way to prevent OS command injection vulnerabilities is to never call out
to OS commands from application-layer code. Instead, implement the required
functionality using safer platform APIs.
    - For example: use **mkdir()** instead of system **("mkdir /dir_name")**
  1. It is required to perform OS commands using user-supplied input, then strong input
validation must be performed.
    - Validate against a whitelist of permitted values.
    - Validate that the input is as expected or valid input.

### Resources

Web Security Academy - OS Command Injection
[https://portswigger.net/web-security/os-command-injection](https://portswigger.net/web-security/os-command-injection)
Web Application Hacker's Handbook
Chapter 10 - Attacking Back-End Components (pgs. 362-368)
Chapter 21 -A Web Application Hacker's Methodology (pgs. pgs. 832-833)
OWASP Command Injection
[https://owasp.org/www-community/attacks/Command_Injection](https://owasp.org/www-community/attacks/Command_Injection)
OWASP os Command Injection Defense Cheat Sheet
[https://cheatsheetseries.owasp.org/cheatsheets/Os_Command_Injection_Defense_Cheat_Sheet.html](https://cheatsheetseries.owasp.org/cheatsheets/Os_Command_Injection_Defense_Cheat_Sheet)
OWASP WSTG Testing for Command Injection
[https://owasp.org/www-project-web-security-testing-guide/latest/4-](https://owasp.org/www-project-web-security-testing-guide/latest/4-)
Web_Application_Security_Testing/07-Input_Validation_Testing/12-Testing_for_Command


