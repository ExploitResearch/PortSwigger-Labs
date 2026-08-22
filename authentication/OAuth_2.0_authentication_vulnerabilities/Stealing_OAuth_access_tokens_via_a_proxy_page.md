# Stealing OAuth access tokens via a proxy page

### Goal -

Solve the PortSwigger lab: Stealing OAuth access tokens via a proxy page


### Vulnerability / Concept

Authentication vulnerabilities allow attackers to compromise user accounts, bypass authentication mechanisms, or enumerate valid usernames. Common flaws include: weak password policies, predictable usernames, brute-force protection bypasses, flawed multi-factor authentication, vulnerable stay-logged-in cookies, password reset poisoning, and OAuth misconfigurations.

The root causes include: relying on client-side validation, inconsistent error messages that reveal account existence, rate-limiting that can be bypassed, password reset mechanisms that trust user input for email generation, and OAuth implementations that don't properly validate redirect URIs.

### Recon / Initial Analysis

1. Test login responses for username enumeration (different messages for valid/invalid usernames)
2. Check response timing differences (valid usernames may take longer to process)
3. Test brute-force protections (IP-based blocking, account lockout, CAPTCHA)
4. Examine stay-logged-in cookies (decode, check if they can be forged)
5. Test password reset flows (email injection, Host header manipulation)
6. For 2FA: test bypass via forced browsing, OTP brute-force, replay attacks
7. For OAuth: test redirect_uri manipulation, access token theft, forced profile linking

### Vulnerability / Concept

Proxy page reflects tokens.

### Exploitation

1. Identify the vulnerability type and injection point
2. Craft the appropriate payload
3. Deliver the payload and verify the result

### Why It Works

The application's authentication mechanism has implementation flaws that allow attackers to either: (1) enumerate valid usernames through differential responses, (2) brute-force passwords by bypassing rate limits, (3) bypass 2FA by skipping the verification step, (4) forge stay-logged-in cookies, or (5) exploit password reset flows via email poisoning.

The broken trust boundary varies: for brute-force, it's the rate-limiting mechanism; for 2FA bypass, it's the state machine; for password reset, it's the email generation logic; for OAuth, it's the redirect_uri validation.

### Real-World Impact

An attacker could:
- Take over any user account by brute-forcing weak passwords
- Bypass 2FA protections on high-value accounts (banking, email, admin)
- Enumerate valid usernames for targeted phishing or social engineering
- Maintain persistent access via forged stay-logged-in cookies
- Hijack OAuth flows to steal access tokens and account credentials
- Reset any user's password by poisoning the reset email link

### Remediation

- Return identical error messages for all authentication failures ('Invalid credentials')
- Implement consistent response timing to prevent timing-based enumeration
- Use strong rate-limiting that cannot be bypassed (per-account and per-IP)
- Require re-authentication for sensitive actions (password change, 2FA setup)
- Use server-generated, unguessable password reset tokens with short expiration
- For OAuth: validate redirect_uri against a strict allowlist, use state parameter for CSRF
- Implement account lockout with automatic unlock after a time period

### Key Takeaways

- Username enumeration is possible through differential responses, timing, or account lockout behavior.
- Brute-force protection must be per-account AND per-IP — neither alone is sufficient.
- 2FA must be enforced server-side — forced browsing must not skip the verification step.
- Password reset tokens must be server-generated, random, and expire quickly.
- OAuth redirect_uri validation must use an exact match, not substring or prefix.
