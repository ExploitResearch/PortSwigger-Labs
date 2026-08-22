# OS Command Injection 

## Contents

- [OS command injection, simple case](./OS_command_injection,_simple_case.md)
- [Blind OS command injection with time delays](./Blind_OS_command_injection_with_time_delays.md)
- [Blind OS command injection with output redirection](./Blind_OS_command_injection_with_output_redirection.md)
- [Blind OS command injection with out-of-band interaction](./Blind_OS_command_injection_with_out-of-band_interaction.md)
- [Blind OS command injection with out-of-band data exfiltration](./Blind_OS_command_injection_with_out-of-band_data_exfiltration.md)

OS command injection is also known as shell injection. It allows an attacker to execute operating system (OS) commands on the server that is running an application, and typically fully compromise the application and its data. Often, an attacker can leverage an OS command injection vulnerability to compromise other parts of the hosting infrastructure, and exploit trust relationships to pivot the attack to other systems within the organization.

The better question is what is command injection? well a command injection is way by which an attacker can execute arbitrary commands because of improper data processing or some vulnerability. A command injection can lead to various attacks like JavaScript code injection, HTML Template injection, etc. One such attack is OS Command Injection. In which attacker can execute arbitrary OS commands on target Operating System or server where application is deployed.

### Types of Command Injection

  1. **In-band Command Injection**
Consists of an attacker executing commands on the host operating system via a vulnerable application and receiving the response of the command in the application.
  1. **Blind/out-of-band Command Injection**
Consists of an attacker executing commands on the host operating system via a vulnerable application that does not return the output from the command within its HTTP response.

|  |  |  |
|---|---|---|
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
- Shell metacharacters: <span style="color: #BE9B00">**&, &&, |, ||, ;, \n, `, $().**</span>
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

![](./images/96035c9c4ae8_001.png)

### **Exploiting Blind Command Injection**

![](./images/96035c9c4ae8_002.png)

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
- For example: use <span style="color: #BE9B00">**mkdir()**</span> instead of system <span style="color: #BE9B00">**("mkdir /dir_name")**</span>
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
