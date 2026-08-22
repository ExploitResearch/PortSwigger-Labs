# Password reset poisoning via middleware

- With Burp running, investigate the password reset functionality.Observe that a link containing a unique reset token is sent via email.
- Send the `POST /forgot-password` request to Burp Repeater. Notice that the `X-Forwarded-Host` header is supported and you can use it to point the dynamically generated reset link to an arbitrary domain.
![](./images/5ccbb779eaf6_001.png)

- notice difference in link normal vs exploited
![](./images/5ccbb779eaf6_002.png)

{% hint style="info" %}
💡 we need to click on manipulated link to see reset token in access log

- Go to the exploit server and make a note of your exploit server URL.
- Go back to the request in Burp Repeater and add the `X-Forwarded-Host` header with your exploit server URL: `X-Forwarded-Host: YOUR-EXPLOIT-SERVER-ID.exploit-server.net`
- Change the `username` parameter to `carlos` and send the request.
- Go to the exploit server and open the access log. You should see a `GET /forgot-password` request, which contains the victim's token as a query parameter. Make a note of this token.
- Go back to your email client and copy the valid password reset link (not the one that points to the exploit server).Paste this into the browser and change the value of the `temp-forgot-password-token` parameter to the value that you stole from the victim.
- Load this URL and set a new password for Carlos's account.
- Log in to Carlos's account using the new password to solve the lab.
{% endhint %}

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab is vulnerable to password reset poisoning via dangling markup. To solve the lab, log in to Carlos's account."

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

An attacker could hijack password reset emails (account takeover), bypass authentication via virtual host routing, perform web cache poisoning, access internal services via SSRF, or poison intermediate caches.

### Detection / Testing Methodology

1. Test if the application accepts arbitrary Host headers
2. Check if password reset emails include the Host header value
3. Test if routing is affected by Host header manipulation
4. Check for duplicate Host headers or X-Forwarded-Host support
5. Test for web cache poisoning via ambiguous Host headers
6. Check if internal services can be accessed via Host header SSRF

### Remediation

- Always validate the Host header against an allowlist of expected domains
- Use server-side configured base URLs for generating links
- Reject requests with duplicate or ambiguous Host headers
- Do not trust X-Forwarded-Host without validation
- Configure the web server to only accept expected virtual hosts
- Use absolute URLs in email templates

### Key Takeaways

- This lab demonstrates a host header vulnerability in a real-world scenario.
- The vulnerability occurs because user input reaches a sensitive operation without proper validation.
- The PortSwigger lab confirms: "This lab is vulnerable to password reset poisoning via dangling markup. To solve the lab, log in to "
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Always validate the Host header against an allowlist of expected domains
