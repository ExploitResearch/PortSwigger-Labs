# Source code disclosure via backup files

### Goal - 

Identify and submit the database password, which is hard-coded in the leaked source code.



### Vulnerability / Concept

This lab demonstrates a vulnerability in the information disclosure category.

This lab leaks its source code via backup files in a hidden directory. To solve the lab, identify and submit the database password, which is hard-coded in the leaked source code.

The vulnerability exists because the application fails to properly validate, sanitize, or secure the user-controlled input that reaches a sensitive operation. The specific attack surface and exploitation technique depend on the exact vulnerability type demonstrated in this lab.

### Recon / Initial Analysis

Based on the lab's objective and the PortSwigger solution:

1. Analyze the application's functionality to identify the attack surface
2. Browse to /robots.txt and notice that it reveals the existence of a /backup directory. Browse to /backup to find the file ProductTemplate.java.bak. Alternatively, right-click on the lab in the site ma
3. Use Burp Suite Proxy to intercept and analyze requests
4. Identify the specific vulnerability type by testing user-controlled input
5. Determine the appropriate exploitation technique for this lab

### Analysis/Exploitation -

When analyzing a web page, one of the first steps is always to check for the existence of a `robots.txt` file.

{% hint style="info" %}
💡 It is a file that requests search engine crawlers to either include or exclude certain parts of the site from their index. Sometimes, interesting locations are revealed.It is up to the crawler whether they obey these wishes or ignore them.
{% endhint %}


In this case, it points straight to the subdirectory `/backup` 

{% hint style="info" %}
💡 (other means to discover it would be tools like Burp Content Discovery, Ffuf, gobuster, wfuzz, ...)
{% endhint %}


Checking the directory shows a backup file for some Java code:

![](./images/2082bf838abe_001.png)

In the code, the credentials for the Postgres database connections can be found:

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab leaks its source code via backup files in a hidden directory. To solve the lab, identify and submit the database password, which is hard-coded in the leaked source code."

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

An attacker could discover internal application structure, source code, database credentials, API keys, configuration files, version information (for CVE exploitation), or bypass authentication using disclosed information.

### Detection / Testing Methodology

1. Check for verbose error messages (submit malformed input, access non-existent resources)
2. Look for debug pages and endpoints (/debug, /admin, /console)
3. Search for backup files (.bak, .old, .swp, ~)
4. Check version control history (.git, .svn)
5. Examine HTTP response headers for version information
6. Test for path traversal to access configuration files
7. Check if stack traces are displayed

### Remediation

- Disable verbose error messages in production (use generic error pages)
- Remove debug pages and endpoints before deployment
- Do not expose backup files, source code, or version control history
- Implement proper access control on all endpoints
- Use a WAF to detect information disclosure patterns
- Regularly audit the application for exposed data

### Key Takeaways

- This lab demonstrates a information disclosure vulnerability in a real-world scenario.
- The vulnerability occurs because user input reaches a sensitive operation without proper validation.
- The PortSwigger lab confirms: "This lab leaks its source code via backup files in a hidden directory. To solve the lab, identify an"
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Disable verbose error messages in production (use generic error pages)
