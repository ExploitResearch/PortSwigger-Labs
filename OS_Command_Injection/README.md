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

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/24e41551-1b5a-441c-af75-c4e724e66e54/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4665E3USIIK%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221956Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCc23zKnyco0xB91vUE6e2jZaUWXQJsPsHfz7jaIAtCqAIgA5du5Fr%2FnHd%2FLZ%2B7lh3GLH74E2AwGR%2FR%2B2d5UYUBJQMqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDFZK4yXb%2FYwTTreklircA0LyHotwKPRnwBV1n3UJ27nNReH4ayGvefBJWHZzWdrzuUufdBqr8OjLfzB9rCkxvUqSTeARcyb8yunFNrDlzggO4FEHYKPw1EYakXjvorEoB0TlkQQLP%2BZOS5493BLg2scIpqclscVtIxJMA7Nn7MhtCAMicAF0tPACbs28Ga0RScLNHRFdyBcQGNg5U4pM%2BPYYIqPjyFfIPciDT%2Fh88LcZEMm3RWZJXFKDwuVE2mRoIkgfZ65pxkzqLa8LUx2ClW7bvSihaZq7%2BLO5Q9HAsLtq0Q1DY7P7bFrmknNba9VEBKgESXshOCjPhZf7zgifwzMSAk2TMlK8vqgfQ5MksKSe02PuRtsYCEP9lmomhVfIvUKaG%2FA8A3JfciRayZ7ORa4rVn0LFglAFarT56mxx15zw1Zhqt8eKcUFTghqywkR4H2cJ%2BOVifR1svTAtt%2F2GzAagIHzrMhHSLSC%2FG8m3B2H26Q5UVH6qAzBxQ8dzVGk%2FYy98LE1OXgPeRQ1w3tJE8vy%2BDqTLE3lrKwvmgP6uSNP6vr%2Fi%2F5soYuY9DfEsggCdaqFNRjP7AnbeYPFrFXy0xvMab6bHZ1ilsFS5wbSXXLTLZ5KnDn0um%2B0PIX3x1EcQTQ7bCqghfQCAHCeMJeEo9QGOqUB0kIKTAcgyWL62%2FN7vTBc%2BeBQkfGT1yzzt%2Fao3QPXASPZDeQZvUNFgR8aKfeNef%2F0rlrDORhGmawWCPO7WxdlKexA7RBoShEUSC%2BSGkJIoQ%2Bc3An0qqA9sPD5sRL7JaRyIuMWsorIJ8yZf7ZdRJz2mtF7T%2FqerA33bVc88QveYm%2BmNoNJ%2FK7rCMzPhYh0jPN%2BRXQI0d6pjiEh9TQHGdVfr%2Fx26YIP&X-Amz-Signature=3cbe75013d9075583852bf95f825fa38f50ac7d649ca80c7ea9bed4dbe25cfac&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

### **Exploiting Blind Command Injection**

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/0db89c61-c15c-45fa-9405-f9e6b2e4fc22/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4665E3USIIK%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221956Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQCc23zKnyco0xB91vUE6e2jZaUWXQJsPsHfz7jaIAtCqAIgA5du5Fr%2FnHd%2FLZ%2B7lh3GLH74E2AwGR%2FR%2B2d5UYUBJQMqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDFZK4yXb%2FYwTTreklircA0LyHotwKPRnwBV1n3UJ27nNReH4ayGvefBJWHZzWdrzuUufdBqr8OjLfzB9rCkxvUqSTeARcyb8yunFNrDlzggO4FEHYKPw1EYakXjvorEoB0TlkQQLP%2BZOS5493BLg2scIpqclscVtIxJMA7Nn7MhtCAMicAF0tPACbs28Ga0RScLNHRFdyBcQGNg5U4pM%2BPYYIqPjyFfIPciDT%2Fh88LcZEMm3RWZJXFKDwuVE2mRoIkgfZ65pxkzqLa8LUx2ClW7bvSihaZq7%2BLO5Q9HAsLtq0Q1DY7P7bFrmknNba9VEBKgESXshOCjPhZf7zgifwzMSAk2TMlK8vqgfQ5MksKSe02PuRtsYCEP9lmomhVfIvUKaG%2FA8A3JfciRayZ7ORa4rVn0LFglAFarT56mxx15zw1Zhqt8eKcUFTghqywkR4H2cJ%2BOVifR1svTAtt%2F2GzAagIHzrMhHSLSC%2FG8m3B2H26Q5UVH6qAzBxQ8dzVGk%2FYy98LE1OXgPeRQ1w3tJE8vy%2BDqTLE3lrKwvmgP6uSNP6vr%2Fi%2F5soYuY9DfEsggCdaqFNRjP7AnbeYPFrFXy0xvMab6bHZ1ilsFS5wbSXXLTLZ5KnDn0um%2B0PIX3x1EcQTQ7bCqghfQCAHCeMJeEo9QGOqUB0kIKTAcgyWL62%2FN7vTBc%2BeBQkfGT1yzzt%2Fao3QPXASPZDeQZvUNFgR8aKfeNef%2F0rlrDORhGmawWCPO7WxdlKexA7RBoShEUSC%2BSGkJIoQ%2Bc3An0qqA9sPD5sRL7JaRyIuMWsorIJ8yZf7ZdRJz2mtF7T%2FqerA33bVc88QveYm%2BmNoNJ%2FK7rCMzPhYh0jPN%2BRXQI0d6pjiEh9TQHGdVfr%2Fx26YIP&X-Amz-Signature=4aa2f7a4cfba0e2455ab47f2b5be611ef803f846e69adae5752db66505ae5728&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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
