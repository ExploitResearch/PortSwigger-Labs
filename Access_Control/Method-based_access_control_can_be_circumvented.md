# Method-based access control can be circumvented

### Target Goal - 

Log in using the credentials `wiener:peter` and exploit the flawed access controls to promote yourself to become an administrator



### Vulnerability / Concept

This lab demonstrates a vulnerability in the access control category.

This lab implements access controls based partly on the HTTP method of requests. You can familiarize yourself with the admin panel by logging in using the credentials administrator:admin.

The vulnerability exists because the application fails to properly validate, sanitize, or secure the user-controlled input that reaches a sensitive operation. The specific attack surface and exploitation technique depend on the exact vulnerability type demonstrated in this lab.

### Recon / Initial Analysis

Based on the lab's objective and the PortSwigger solution:

1. Analyze the application's functionality to identify the attack surface
2. Log in using the admin credentials.
                    
                    
                        Browse to the admin panel, promote carlos, and send the HTTP request to Burp Repeater.
           
3. Use Burp Suite Proxy to intercept and analyze requests
4. Identify the specific vulnerability type by testing user-controlled input
5. Determine the appropriate exploitation technique for this lab

### Analysis/Exploitation -

<details><summary>Summary</summary>

We can see this request with administrator user.

```text
POST /admin-roles HTTP/1.1
...
username=carlos&action=upgrade

```

```text

POST /admin-roles - HTTP/1.1   -->401 Unauthorized
GET /admin - HTTP/1.1   -->400 Missing parameter'username'
```

With non privileged user, we  get 401 Unauthorized error.

But we can bypass the error with another type of request instead of using POST.

```text
GET /admin-roles?username=wiener&action=upgrade HTTP/1.1 --> 302 Found
GET /admin --> 200 OK
```

</details>

familiarize yourself with the admin panel by logging in using the credentials `administrator:admin` 

![](./images/730f8a45256c_001.png)

Here, administrator can upgrade or downgrade a user.

When we try to upgrade a user:

![](./images/730f8a45256c_002.png)

**It’s sending a POST request to **`/admin-roles`**, and with the **`username`** and **`action`**.**

Now, let’s log out and login as user `wiener` to do vertical privilege escalation!

After login send any GET request to repeater and change the ** **location to** **`/admin-roles`

![](./images/730f8a45256c_003.png)

As you can see, looks like we can access `/admin-roles` when we’re sending a GET request to `/admin-roles` without any parameters.

If we change it to POST method we  get 401 Unauthorized . **So we’re allowed to send a GET request to **`/admin-roles`

![](./images/730f8a45256c_004.png)

**send a GET request to **`/admin-roles`**, with parameters: **`username=wiener&action=upgrade`**:**

![](./images/730f8a45256c_005.png)

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab implements access controls based partly on the HTTP method of requests. You can familiarize yourself with the admin panel by logging in using the credentials administrator:admin."

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
- The PortSwigger lab confirms: "This lab implements access controls based partly on the HTTP method of requests. You can familiarize"
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Implement server-side authorization checks on every request
