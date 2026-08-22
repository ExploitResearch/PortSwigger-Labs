# SameSite Lax bypass via cookie refresh

### Goal -

Bypass SameSite=Lax cookie restrictions to perform a CSRF attack.

### Exploitation

1. Identify that the target cookie has SameSite=Lax
2. Find a GET endpoint that refreshes/re-issues the session cookie
3. Use a top-level navigation to trigger the cookie refresh
4. The refreshed cookie may have SameSite=None or Lax for a brief window
5. Immediately perform the CSRF attack while the cookie is in the relaxed state
