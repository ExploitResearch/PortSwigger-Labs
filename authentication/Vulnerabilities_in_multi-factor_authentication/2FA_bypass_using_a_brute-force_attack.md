# 2FA bypass using a brute-force attack

### Goal -

Solve the PortSwigger lab: 2FA bypass using a brute-force attack

### Vulnerability / Concept

The 2FA implementation may be vulnerable to brute-force if it doesn't rate-limit OTP submission. By trying all possible codes, an attacker can bypass the 2FA.

### Exploitation

1. Login with valid credentials
2. Capture the OTP submission request in Burp
3. Use Burp Intruder to brute-force the OTP code
4. Look for a different response (302 redirect) indicating success

### Why It Works

The application doesn't rate-limit or lock out after failed OTP attempts, allowing a brute-force attack to eventually find the correct code.

### Key Takeaways

- Rate-limit OTP submissions (max 5 attempts)
- Lock the account after too many failures
- Use TOTP with sufficient entropy (6+ digits)
