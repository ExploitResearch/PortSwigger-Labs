# Multi-step process with no access control on one step

### Target Goal - 

Log in using the credentials `wiener:peter` and exploit the flawed access controls to promote yourself to become an administrator



### Vulnerability / Concept

This lab demonstrates a vulnerability in the access control category.

This lab has an admin panel with a flawed multi-step process for changing a user's role. You can familiarize yourself with the admin panel by logging in using the credentials administrator:admin.

The vulnerability exists because the application fails to properly validate, sanitize, or secure the user-controlled input that reaches a sensitive operation. The specific attack surface and exploitation technique depend on the exact vulnerability type demonstrated in this lab.

### Recon / Initial Analysis

Based on the lab's objective and the PortSwigger solution:

1. Analyze the application's functionality to identify the attack surface
2. Log in using the admin credentials.
                    
                    
                        Browse to the admin panel, promote carlos, and send the confirmation HTTP request to Burp Repeater
3. Use Burp Suite Proxy to intercept and analyze requests
4. Identify the specific vulnerability type by testing user-controlled input
5. Determine the appropriate exploitation technique for this lab

### Analysis/Exploitation -

**Let’s login as **`administrator`

**Browse to the admin panel, promote **`carlos`

When administrator try to upgrade a user, it’ll send a POST request to `/admin-roles`, with parameter: `username` and `action` (`upgrade`/`downgrade`).

![](./images/9479c2d43281_001.png)

After sending a POST request, a confirm page will be prompt, If we click `Yes`, it’ll send a POST request again:

However, this time we see 1 more parameter: `confirmed` is set to `true`.

![](./images/9479c2d43281_002.png)

**send the both steps POST request to Burp Repeater.**

With above information, we can login as user `wiener`, and try to escalate our privilege to administrator:

![](./images/9479c2d43281_003.png)

copy wiener’s session id 

Change the session id and username to wiener in both steps post request which we send to repeater

![](./images/9479c2d43281_004.png)

in first step we get unauthorized

![](./images/9479c2d43281_005.png)

**But the back-end doesn’t check the second step in upgrading a user’s privilege**

Response displays 302 Found with directory location /admin, which means the URL function has successfully upgraded the user with username wiener to admin.

refresh the page to see we’re an administrator or not

The admin panel shows that the wiener account has been promoted to admin.

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab has an admin panel with a flawed multi-step process for changing a user's role. You can familiarize yourself with the admin panel by logging in using the credentials administrator:admin."

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

An attacker could access other users' personal data, gain administrative access, delete or modify other users' data, bypass paywalls or subscription requirements, or perform actions reserved for privileged users.

### Detection / Testing Methodology

1. Map all functionality available to different user roles
2. Check if admin interfaces are discoverable (robots.txt, JS files, predictable URLs)
3. Test if user roles can be changed via request parameters
4. Identify user IDs in URLs and test if they can be changed (IDOR)
5. Test multi-step processes for missing access control on individual steps
6. Compare authenticated vs unauthenticated access

### Remediation

- Implement server-side authorization checks on every request
- Never trust client-side parameters for role/privilege determination
- Use indirect object references (map user-supplied IDs to session-scoped references)
- Verify authorization on every step of multi-step processes
- Do not use Referer headers for access control
- Implement deny-by-default authorization

### Key Takeaways

- This lab demonstrates a access control vulnerability in a real-world scenario.
- The vulnerability occurs because user input reaches a sensitive operation without proper validation.
- The PortSwigger lab confirms: "This lab has an admin panel with a flawed multi-step process for changing a user's role. You can fam"
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Implement server-side authorization checks on every request
