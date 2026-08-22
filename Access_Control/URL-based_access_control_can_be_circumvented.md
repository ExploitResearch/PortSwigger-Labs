# URL-based access control can be circumvented

### Target Goal - 

Access the admin panel and delete the user `carlos`.



### Vulnerability / Concept

This lab demonstrates a vulnerability in the access control category.

To solve the lab, access the admin panel and delete the user carlos.

The vulnerability exists because the application fails to properly validate, sanitize, or secure the user-controlled input that reaches a sensitive operation. The specific attack surface and exploitation technique depend on the exact vulnerability type demonstrated in this lab.

### Recon / Initial Analysis

Based on the lab's objective and the PortSwigger solution:

1. Analyze the application's functionality to identify the attack surface
2. Try to load /admin and observe that you get blocked. Notice that the response is very plain, suggesting it may originate from a front-end system.
                    
                    
            
3. Use Burp Suite Proxy to intercept and analyze requests
4. Identify the specific vulnerability type by testing user-controlled input
5. Determine the appropriate exploitation technique for this lab

### Analysis/Exploitation -

there are navbar contents consisting of Home, Admin Panel, and My Account.When trying to access the Admin Panel, the web display the text “access denied”.

![](./images/de1f871fd5cb_001.png)

Let’s try to intercept when we want to access the admin panel using the burp suite. Here’s how it looks.

![](./images/de1f871fd5cb_002.png)

Based on the intercept results, the HTTP request method “Get” points to the /admin directory.

Let’s try to use non-standard HTTP headers that can replace the URL in the original request such as X-Original-URL to bypass admin access.

![](./images/de1f871fd5cb_003.png)

It still doesn’t work :(

According to the lab description, “the front-end system has been configured to block external access to that path”. Let’s try to remove “admin” in the HTTP request method “get” so that it only leaves “/”.

![](./images/de1f871fd5cb_004.png)

The response displays 200 OK, which means the admin access was successfully bypassed. Next, find out how to delete the user Carlos to complete this lab.

Search “delete” or scroll down a bit in the response. We will find the path “/admin/delete” with the query string “?username=carlos” which leads to the user data deletion function with the parameter “username” which is “Carlos”.

![](./images/de1f871fd5cb_005.png)

Let’s try adding it to the X-Original-Url and run it.

![](./images/de1f871fd5cb_006.png)

The response will show “HTTP/2 400 Bad Request” with the message “Missing parameter ‘username’”. This indicates that the server did not read the query string “?username=carlos” in the X-Original-Url. So for the query string, we can try moving it to Get /?username=carlos.

![](./images/de1f871fd5cb_007.png)

The response displays 302 Found with the directory location /admin, which means the URL function has successfully deleted the user with the username Carlos.

If we check back to the /admin directory, the Carlos user no longer exists.

![](./images/de1f871fd5cb_008.png)

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "To solve the lab, access the admin panel and delete the user carlos."

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
- The PortSwigger lab confirms: "To solve the lab, access the admin panel and delete the user carlos."
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Implement server-side authorization checks on every request
