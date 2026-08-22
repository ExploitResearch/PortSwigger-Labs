# 2FA bypass using a brute-force attack

### Goal -

Solve the PortSwigger lab: 2FA bypass using a brute-force attack

### Exploitation

1. Login with valid credentials
2. Capture the OTP submission request in Burp
3. Use Burp Intruder to brute-force the OTP code
4. Look for a different response (302 redirect) indicating success

### Why It Works

The exploit succeeds because this lab's two-factor authentication is vulnerable to brute-forcing. you have already obtained a valid username and password, but do not have access to the user's 2fa verification code. to solve the l

The official solution confirms: With Burp running, log in as carlos and investigate the 2FA verification process. Notice that if you enter the wrong code twice, you will be logged ou

The root cause is a failure in the application's security architecture specific to this authentication scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab's two-factor authentication is vulnerable to brute-forcing. You have already obtained a val"
- Consistent error messages and rate-limiting prevent enumeration and brute-force.
