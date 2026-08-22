# Bypassing SameSite Cookie Restrictions

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

![](../images/bddb838ab550_001.png)

Two URLs are considered to have the **same site** if they share the exact same scheme and domain name(TLD & TLD+1).

Two URLs are considered to have the **same origin **if they share the exact same scheme, domain name, and port.

The labs below demonstrate ways to bypass SameSite cookie restrictions when
the application relies on SameSite attributes for CSRF protection.

## Labs

- [SameSite Lax bypass via method override](./SameSite_Lax_bypass_via_method_override.md)
- [SameSite Strict bypass via client-side redirect](./SameSite_Strict_bypass_via_client-side_redirect.md)
- [SameSite Strict bypass via sibling domain](./SameSite_Strict_bypass_via_sibling_domain.md)
- [SameSite Lax bypass via cookie refresh](./SameSite_Lax_bypass_via_cookie_refresh.md)
