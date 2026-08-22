# CSRF

## Contents

- [CSRF vulnerability with no defenses](./CSRF_vulnerability_with_no_defenses.md)
- [CSRF where token validation depends on request method](./CSRF_where_token_validation_depends_on_request_method.md)
- [CSRF where token validation depends on token being present](./CSRF_where_token_validation_depends_on_token_being_present.md)
- [CSRF where token is not tied to user session](./CSRF_where_token_is_not_tied_to_user_session.md)
- [CSRF where token is tied to non-session cookie](./CSRF_where_token_is_tied_to_non-session_cookie.md)
- [CSRF where token is duplicated in cookie](./CSRF_where_token_is_duplicated_in_cookie.md)
- [SameSite Lax bypass via method override](./SameSite_Lax_bypass_via_method_override.md)
- [SameSite Strict bypass via client-side redirect](./SameSite_Strict_bypass_via_client-side_redirect.md)
- [SameSite Strict bypass via sibling domain](./SameSite_Strict_bypass_via_sibling_domain.md)
- [SameSite Lax bypass via cookie refresh](./SameSite_Lax_bypass_via_cookie_refresh.md)
- [CSRF where Referer validation depends on header being present](./CSRF_where_Referer_validation_depends_on_header_being_present.md)
- [CSRF with broken Referer validation](./CSRF_with_broken_Referer_validation.md)

### About CSRF

CSRF stands for Cross-Site Request Forgery. It is a type of web security vulnerability where an attacker tricks a user's browser into making an unintended and potentially malicious request on a trusted website where the user is authenticated. The attack takes advantage of the fact that web browsers automatically include any relevant cookies for a specific domain with every HTTP request, even if those requests are initiated by malicious websites.

### Here's a basic overview of how CSRF attacks work: 

  1. **Authentication Cookies:** When a user logs into a website, they receive a session cookie that authenticates their session. This cookie is automatically sent with each subsequent request to the same domain.
  1. **Malicious Request:** An attacker tricks a user into visiting a malicious website or clicking on a malicious link that initiates a request to a trusted website where the user is already authenticated. The attacker crafts a request that performs an action on the target site, such as changing the user's password, transferring funds, or making some other unintended modification.
  1. **Automatic Inclusion of Cookies:** Because the user is already authenticated on the target site, their browser automatically includes the session cookie with the malicious request.
  1. **Unintended Action:** The malicious request is processed by the target site, and since the request contains the user's authentication credentials, the site treats it as a legitimate request from the authenticated user, leading to the unintended action being performed.

### To protect against CSRF attacks, web developers can implement countermeasures such as:

  - **Anti-CSRF Tokens:** Include unique tokens in forms or requests that are checked by the server to ensure that the request is legitimate and originated from the expected source.
    - CSRF tokens should contain significant entropy and be strongly unpredictable, with the same properties as session tokens in general.
    - CSRF tokens should be treated as secrets and handled in a secure manner throughout their lifecycle. An approach that is normally effective is to transmit the token to the client within a hidden field of an HTML form that is submitted using the POST method.
    - When a CSRF token is generated, it should be stored server-side within the user's session data. When a subsequent request is received that requires validation, the server- side application should verify that the request includes a token which matches the value that was stored in the user's session.
  - **SameSite Cookies:** Use the SameSite attribute for cookies to control when cookies are sent with cross-site requests.
Ideally, you should use the Strict policy by default, then lower this to Lax only if you have a good reason to do so. Never disable SameSite restrictions with SameSite=None unless you're fully aware of the security implications.

  - **Custom Headers:** Use custom headers that are required for requests to be processed, making it harder for an attacker to forge a request.
  - **Requiring Reauthentication:** Sensitive actions can be protected by requiring the user to reauthenticate before performing them.
  - **Avoid Cookie Auth: **Use token-based authentication (e.g., JWT, OAuth) instead of session cookies.
  - **Strict Content-Type: **Enforce application/json or non-browser-friendly types to block simple form submissions.

### For a CSRF attack to be possible, three key conditions must be in place:

  - **A relevant action.** There is an action within the application that the attacker has a reason to induce. This might be a privileged action (such as modifying permissions for other users) or any action on user-specific data (such as changing the user's own password).
  - **Cookie-based session handling.**
Performing the action involves issuing one or more HTTP requests, and the application relies solely on session cookies to identify the user who has made the requests. There is no other mechanism in place for tracking sessions or validating user requests.
  - **No unpredictable request parameters.**
The requests that perform the action do not contain any parameters whose values the attacker cannot determine or guess. For example, when causing a user to change their password, the function is not vulnerable if an attacker needs to know the value of the existing password.

### CSRF VS XSS

  - CSRF is often considered a "one-way" attack, meaning the attacker cannot see the response to the forged request, while XSS is "two-way" as the attacker can control the script's behavior.The attacker's injected script can issue arbitrary requests, read the responses, and exfiltrate data to an external domain of the attacker's choosing.
  - CSRF requires the victim to be logged in, while XSS does not.

|  |  |  |
|---|---|---|
| **Aspect** | **Cross-Site Scripting (XSS)** | **Cross-Site Request Forgery (CSRF)** |
| **Definition** | Vulnerability where malicious scripts are injected into web pages viewed by victim users and executed in the victim's browser. | Vulnerability where an attacker tricks a user's browser into making unintended requests to a trusted site where the user is authenticated. |
| **Target** | The victim's browser. | The trusted website where the victim is logged in. |
| **Goal** | Execute scripts within the victim's browser context. | Perform actions on behalf of an authenticated user without their knowledge or consent. |
| **Attack Vector** | Injecting malicious code into user inputs (e.g., input fields, URL parameters). | Inducing the victim to unknowingly send requests to a trusted site (e.g., via malicious links, image tags). |
| **Mitigation** | Input validation, sanitization, and Content Security Policy (CSP) headers. | Anti-CSRF tokens, SameSite cookies, custom headers, and reauthentication for sensitive actions. |

## Manual Testing Steps

- **Identify state-changing requests:** Focus on HTTP requests that modify data or perform actions (e.g., POST, PUT, DELETE).
- **Check for anti-CSRF tokens:** Verify if requests include anti-CSRF tokens in headers, body, or URL parameters. Absence or improper validation indicates vulnerability.
- **Craft CSRF Proof of Concept (PoC):**
Create an HTML form or script that replicates the target request without the user's consent. Host this PoC and test if the action executes when accessed by an authenticated user.
- **Test token validation:** Modify or omit the anti-CSRF token in requests to see if the server still accepts them, indicating weak or missing validation.
- **Check HTTP methods and content types:** Some APIs accept only JSON or specific methods; try changing methods or content types (e.g., using `enctype="text/plain"`) to bypass protections.

### CSRF token

A CSRF token is a unique, secret, and unpredictable value that is generated by the server-side application and shared with the client. When issuing a request to perform a sensitive action

###  **SameSite cookie restrictions**

The SameSite attribute is used in HTTP cookies to control whether the browser should include the cookie in third-party requests. This attribute helps prevent certain types of cross-site request forgery (CSRF) and cross-site scripting (XSS) attacks by restricting when cookies are sent with cross-site requests.

The SameSite attribute can have three values:

  1. **SameSite=None:**
    - Cookies with this attribute can be sent with both same-site and cross-site requests.
    - Requires the Secure attribute, meaning the cookie will only be sent over HTTPS connections.
  1. **SameSite=Lax:**
    - Cookies are not sent with cross-site requests triggered by a top-level navigation (e.g., clicking a link).
    - Cross-site requests initiated by third-party elements, such as images or scripts, do not include the cookie.
  1. **SameSite=Strict:**
    - Cookies are not sent with any cross-site requests, regardless of the context.
    - This provides the highest level of security but may impact some legitimate use cases.

![](./images/bddb838ab550_001.png)

Two URLs are considered to have the **same site** if they share the exact same scheme and domain name(TLD & TLD+1).

Two URLs are considered to have the **same origin **if they share the exact same scheme, domain name, and port.

### Referrer Based Validation

The HTTP Referrer header (which is inadvertently misspelled in the HTTP specification) is an optional request header that contains the URL of the web page that linked to the resource that is being requested. It is generally added automatically by browsers when a user triggers an HTTP request, including by clicking a link or submitting a form. Various methods exist that allow the linking page to withhold or modify the value of the Referer header. This is often done for privacy reasons.

### Is CSRF possible in API?

|  |  |
|---|---|
| **When CSRF is Possible** | - API uses **cookie-based authentication** (e.g., session cookies) |
|  | - API accepts state-changing HTTP methods (POST, PUT, DELETE) |
|  | - API is accessed via browsers that automatically send cookies |
| **When CSRF is Not Possible** | - API uses **token-based authentication** (e.g., Bearer tokens in Authorization header) |
|  | - API is accessed by non-browser clients (mobile apps, servers) |
|  | - API requires explicit tokens or headers not automatically sent by browsers |

Is CSRF finding valid in a application where only search funtionality is present—> to get some data?

[https://teams.microsoft.com/l/meetup-join/19%3Ameeting_MjkxMmI2NDUtMjc0ZS00M2NmLWIyYzAtZDkwYzM3NjdmN2Nh%40thread.v2/0?context={"Tid"%3A"396b38cc-aa65-492b-bb0e-3d94ed25a97b"%2C"Oid"%3A"85e14178-1d13-413f-a089-31a33c327658"}](https://teams.microsoft.com/l/meetup-join/19%3ameeting_MjkxMmI2NDUtMjc0ZS00M2NmLWIyYzAtZDkwYzM3NjdmN2Nh%40thread.v2/0?context=%7B%22Tid%22%3A%22396b38cc-aa65-492b-bb0e-3d94ed25a97b%22%2C%22Oid%22%3A%2285e14178-1d13-413f-a089-31a33c327658%22%7D)
