# 2FA bypass using a brute-force attack

**Lab URL:** https://portswigger.net/web-security/authentication/multi-factor/lab-2fa-bypass-using-a-brute-force-attack

### Goal -

Solve the PortSwigger lab: 2FA bypass using a brute-force attack

### Exploitation

1. Login with valid credentials
2. Capture the OTP submission request in Burp
3. Use Burp Intruder to brute-force the OTP code
4. Look for a different response (302 redirect) indicating success
