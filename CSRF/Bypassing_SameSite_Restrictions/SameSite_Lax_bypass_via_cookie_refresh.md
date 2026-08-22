# SameSite Lax bypass via cookie refresh

### Goal -

Bypass SameSite=Lax cookie restrictions to perform a CSRF attack.

### Vulnerability / Concept

SameSite=Lax cookies are sent with top-level GET navigations. The application may have a cookie refresh mechanism that causes a new cookie to be issued with a short-lived SameSite=None setting.

### Exploitation

1. Identify that the target cookie has SameSite=Lax
2. Find a GET endpoint that refreshes/re-issues the session cookie
3. Use a top-level navigation to trigger the cookie refresh
4. The refreshed cookie may have SameSite=None or Lax for a brief window
5. Immediately perform the CSRF attack while the cookie is in the relaxed state

### Why It Works

SameSite=Lax allows cookies in top-level GET navigations but blocks them in cross-site POST requests. However, if the application re-issues the cookie with a different SameSite setting during a GET request, the attacker can exploit the brief window to perform the CSRF attack.

### Key Takeaways

- SameSite=Lax is not a complete CSRF defense
- Cookie refresh mechanisms can weaken SameSite protections
- Use CSRF tokens in addition to SameSite
- Set SameSite=Strict for sensitive cookies
