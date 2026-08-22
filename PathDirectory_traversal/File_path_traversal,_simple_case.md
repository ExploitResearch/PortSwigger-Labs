# File path traversal, simple case

### Goal - 

Retrieve the contents of the `/etc/passwd` file.


### Vulnerability / Concept

This lab demonstrates a web security vulnerability that can be exploited to compromise the application's security. The vulnerability allows an attacker to bypass security controls and perform unauthorized actions.

The core issue is a failure in the application's security architecture — either insufficient input validation, broken access controls, improper trust boundaries, or insecure handling of user-supplied data. Understanding the root cause is essential for both exploitation and remediation.

### Recon / Initial Analysis

1. Identify the attack surface — what user-controlled inputs exist (URL parameters, form fields, headers, cookies)
2. Analyze the application's behavior with unexpected input
3. Map the request flow and identify trust boundaries
4. Test for error messages that reveal implementation details
5. Compare authenticated vs unauthenticated behavior
6. Use Burp Suite Proxy to capture and analyze all requests
7. Check for hidden parameters using Burp Intruder or Param Miner

### Analysis/Exploitation 

When checking the source of the page, The product images are given as explicit file names in URL arguments to `/image`:

![](./images/e46c19db7688_001.png)

Calling this URL directly in the browser (e.g. `https://ac301f701f93c15d803e3c72008500ed.web-security-academy.net/image?filename=39.jpg`) will display just the image.

or open any image in new tab

![](./images/e46c19db7688_002.png)

**Intercept the request via Burp Suite and send to repeater:**

![](./images/e46c19db7688_003.png)

If you don't see it in the `HTTP history`, check if images are filtered out in the filter bar (by default it is hidden):

![](./images/e46c19db7688_004.png)

**use the **`../`** to move up a directory level and try to retrieve **`/etc/passwd`** file?**

![](./images/e46c19db7688_005.png)

**When we move up 1 directory level, it outputs **`No such file`**. Let’s move up more directory levels until we retrieved the **`/etc/passwd`** file!**

![](./images/e46c19db7688_006.png)

**When we move up 3 directory levels, it sucessfully retrieved the **`/etc/passwd`**’s content!!**

{% hint style="info" %}
💡 Start by using `/etc/passwd` as filename and adding some `../` to the beginning. With `../../etc/passwd` it gives a `"No such file"` error, but once I go three levels up, this changes and we get file content
{% endhint %}

### Why It Works

The vulnerability exists because the application fails to properly validate, sanitize, or authorize user input. The broken trust boundary allows an attacker to manipulate the application's behavior by injecting unexpected data that the server processes without adequate security checks.

### Real-World Impact

An attacker could exploit this vulnerability to:
- Access sensitive data belonging to other users
- Bypass authentication or authorization controls
- Perform unauthorized actions on behalf of legitimate users
- Potentially achieve remote code execution on the server
- Compromise the integrity or availability of the application

### Remediation

- Implement proper server-side input validation for all user-controlled data
- Use parameterized queries and prepared statements
- Enforce server-side authorization checks on every request
- Follow the principle of least privilege
- Implement security headers (CSP, X-Frame-Options, X-Content-Type-Options)
- Use a Web Application Firewall (WAF) as defense-in-depth
- Regularly test for vulnerabilities using automated scanners and manual testing

### Key Takeaways

- Never trust user-controlled input — validate and sanitize everything server-side.
- Security controls must be enforced server-side, not client-side.
- Understanding the vulnerability's root cause is essential for proper remediation.
- Burp Suite is essential for identifying and exploiting web vulnerabilities.
- Defense in depth — use multiple layers of protection, not just one.
