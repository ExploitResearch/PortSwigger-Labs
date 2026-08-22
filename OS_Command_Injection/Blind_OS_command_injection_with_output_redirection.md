# Blind OS command injection with output redirection

### Goal - 

Exploit the blind command injection and redirect the output from the whoami command to the /var/www/images


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

{% hint style="info" %}
💡 You can redirect the output from the injected command into a file within the web root that you can access then retrieve using the browser. 
For example, if the application serves static resources from the filesystem location `/var/www/static`, then you can submit the following input:

```bash
& whoami > /var/www/static/whoami.txt &
```

The `>` character sends the output from the `whoami` command to the specified file. You can then use the browser to fetch `https://vulnerable-website.com/whoami.txt` to retrieve the file, and view the output from the injected command.

{% endhint %}


In the previous lab, we found that the `email` parameter is vulnerable to blind OS command injection:

![](./images/9ac789e31ef7_001.png)

Now, instead of triggering a time delay, we can also **redirect the command’s output to a file, and stored it to where we can access.**

In the home page, we can see there are some product images:

Typically you’ll **stored the output to a static file**, like `images`.As we can see, **they are at **`/image`**.**

![](./images/9ac789e31ef7_002.png)

To redirect command’s output to a file, we can put it to `/var/www/image/<filename>`.since it is mentionted in lab description that Writeable folder is at `/var/www/images/`

{% hint style="info" %}
**Note: **In Linux, web root is usually located in <span style="color: #E03E1B">**/var/www/**</span>.

The command to execute is `whoami > /var/www/images/whoami.txt `to write the file. Inject it into the email argument. And as in the previous lab, commenting out the remainder results in a `200 OK`, while not doing so results in `500 Internal Server Error`. Both ways work though.

![](./images/9ac789e31ef7_003.png)

**Access the file**

Now the file is in `/var/www/images`, but the path to it within the application is unknown and perhaps not even accessible directly. But I can utilize the way the application includes its images with a GET request to `/image?filename=`

![](./images/9ac789e31ef7_004.png)
{% endhint %}

{% hint style="info" %}
💡 **summary
**

  1. Find & Confirm blind command injection
-email field
  1. Check location from where application serves static resources, here images 
  1. Redirect output to file at that static location
  1. Check if file was created by accessing it

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
