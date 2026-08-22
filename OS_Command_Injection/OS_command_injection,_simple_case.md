# OS command injection, simple case

### Goal - 

Exploit command injection to execute whoami command.



### Vulnerability / Concept

This lab demonstrates a vulnerability in the os command injection category.

This lab contains an OS command injection vulnerability in the product stock checker.

The vulnerability exists because the application fails to properly validate, sanitize, or secure the user-controlled input that reaches a sensitive operation. The specific attack surface and exploitation technique depend on the exact vulnerability type demonstrated in this lab.

### Recon / Initial Analysis

Based on the lab's objective and the PortSwigger solution:

1. Analyze the application's functionality to identify the attack surface
2. Use Burp Suite to intercept and modify a request that checks the stock level.
                    
                    
                        Modify the storeID parameter, giving it the value 1|whoa
3. Use Burp Suite Proxy to intercept and analyze requests
4. Identify the specific vulnerability type by testing user-controlled input
5. Determine the appropriate exploitation technique for this lab

### Analysis/Exploitation 

As usual, the first step is to browse around a bit. Upon viewing view details of an product we get detail information about that product and we can see upon visiting a specific product a parameter named **productId **is being set. Well this is where we can try to preform command injection and i did but no luck because it fetches information by using an API which restrict all special characters. But as there is another functionality which allows us check for availability of stocks.

Let’s click the `Check stock` button, and intercept the request via Burp Suite

When we clicked that button, it’ll send a POST request to `/product/stock`, with parameter `productId=1` and `storeId=1`.

![](./images/d7cdbb616498_001.png)

As we have two parameters, I try to inject both with different commands. This way, I can find out which parameter is injectable and in which order they are executed.

{% hint style="info" %}
💡 The script call might look something like this (likely not the exact syntax, but the general idea is the same):

```bash
echo system("someScript.sh $_REQUEST['productID'] $_REQUEST['storeId']")
```

In this case, the parameters are used as arguments for the script and the output is directly echoed back into the HTML.

There are multiple ways to execute multiple commands in one line in a shell, separating the individual commands with for example `&`, `&&`, `|`, `||`, `;`. All behave slightly differently. On Unix systems, my favorite is `;` as it completely separates the commands without side effects based on return conditions or execution order. In some conditions `&` is better as it backgrounds the command before my injection and runs my code without waiting for the other command to finish. Still, my favourite remains `;`.

<span style="color: #E03E1B">**NOTE :**</span>** when using **`&`**, it must be URLencoded**

{% endhint %}


![](./images/d7cdbb616498_002.png)

From the response, it can be seen that both parameters are injectable, and they are executed in the order productId first, storeId second.

**Let’s execute **`whoami`** command**

comment out the remainder of the line after the `whoami` to avoid the error message of the second parameter:

![](./images/d7cdbb616498_003.png)

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab contains an OS command injection vulnerability in the product stock checker."

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
- The PortSwigger lab confirms: "This lab contains an OS command injection vulnerability in the product stock checker."
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Use parameterized APIs instead of shell commands (e.g., exec() with argument arrays)
