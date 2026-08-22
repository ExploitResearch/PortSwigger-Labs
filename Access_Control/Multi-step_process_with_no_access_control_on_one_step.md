# Multi-step process with no access control on one step

### Target Goal - 

Log in using the credentials `wiener:peter` and exploit the flawed access controls to promote yourself to become an administrator


### Vulnerability / Concept

Access control vulnerabilities occur when an application does not properly enforce restrictions on what authenticated users are allowed to do. These include: horizontal privilege escalation (accessing another user's data), vertical privilege escalation (accessing admin functionality as a regular user), and insecure direct object references (IDOR).

Common flaws include: unprotected admin interfaces, user roles controlled by client-side parameters, user IDs in URLs without authorization checks, and multi-step processes that skip access control on certain steps.

The root cause is always the same: the server trusts client-supplied data (URLs, parameters, cookies, headers) to determine authorization without server-side validation.

### Recon / Initial Analysis

1. Map all functionality available to different user roles (regular user vs admin)
2. Check if admin interfaces are discoverable (robots.txt, JavaScript files, predictable URLs)
3. Test if user roles can be changed via request parameters (role=admin, isAdmin=true)
4. Identify user IDs in URLs and test if they can be changed to access other users' data
5. Test multi-step processes for missing access control on individual steps
6. Check if the Referer header is used for access control (easily spoofed)
7. Compare authenticated vs unauthenticated access to endpoints

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

The application fails to enforce server-side authorization checks. Instead of verifying that the current user has permission to perform the requested action, it either: (1) doesn't check at all, (2) relies on client-side parameters that can be modified, (3) checks authorization on some steps but not others, or (4) uses insecure mechanisms like Referer headers.

The broken trust boundary is between the authentication system and the authorization system: the application knows who the user is but doesn't verify what they're allowed to do.

### Real-World Impact

An attacker could:
- Access other users' personal data, orders, messages, and payment information
- Gain administrative access to the entire application
- Delete or modify other users' data
- Perform actions reserved for privileged users (account deletion, system configuration)
- Bypass paywalls or subscription requirements

### Remediation

- Implement server-side authorization checks on every request, not just the initial page load
- Never trust client-side parameters for role or privilege determination
- Use indirect object references (map user-supplied IDs to session-scoped references)
- Verify authorization on every step of multi-step processes
- Do not use Referer headers for access control
- Implement role-based access control (RBAC) with server-side enforcement
- Deny by default — require explicit permission grants

### Key Takeaways

- Access control must be enforced server-side on every request — client-side controls are bypassable.
- User IDs in URLs (IDOR) require server-side verification that the user owns the resource.
- Multi-step processes must enforce access control on every step, not just the first.
- Admin interfaces must not be discoverable by regular users — use server-side role checks.
- Never use the Referer header for authorization — it's client-controlled and spoofable.
