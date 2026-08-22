# User role controlled by request parameter

### Target Goal - 

Access the admin panel and use it to delete the user `carlos`



### Vulnerability / Concept

This lab demonstrates a vulnerability in the access control category.

This lab has an admin panel at /admin, which identifies administrators using a forgeable cookie.

The vulnerability exists because the application fails to properly validate, sanitize, or secure the user-controlled input that reaches a sensitive operation. The specific attack surface and exploitation technique depend on the exact vulnerability type demonstrated in this lab.

### Recon / Initial Analysis

Based on the lab's objective and the PortSwigger solution:

1. Analyze the application's functionality to identify the attack surface
2. Browse to /admin and observe that you can't access the admin panel.
                    
                    
                        Browse to the login page.
                    
                   
3. Use Burp Suite Proxy to intercept and analyze requests
4. Identify the specific vulnerability type by testing user-controlled input
5. Determine the appropriate exploitation technique for this lab

### Analysis/Exploitation -

Browse to `/admin` and observe that you can't access the admin panel.

![](./images/31af54ec147f_001.png)

Turn on inercept and **Login as user **`wiener`**:**

Observe that the response sets the cookie `Admin=false`. Change it to `Admin=true`

![](./images/31af54ec147f_002.png)

There is a cookie called `Admin`, and it’s value is `false`**change the value to **`true`

![](./images/31af54ec147f_003.png)

Load the admin panel and delete `carlos`.

![](./images/31af54ec147f_004.png)

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab has an admin panel at /admin, which identifies administrators using a forgeable cookie."

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
- The PortSwigger lab confirms: "This lab has an admin panel at /admin, which identifies administrators using a forgeable cookie."
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Implement server-side authorization checks on every request
