# Username enumeration via different responses

### Goal -

Enumerate valid usernames by observing differences in the application's response to login attempts with valid vs. invalid usernames.

### Vulnerability / Concept

The application returns different responses (different messages, status codes, or timing) depending on whether the username exists. This allows an attacker to enumerate valid usernames.

### Exploitation

1. Attempt login with a known valid username and an invalid password
2. Attempt login with a random invalid username and the same password
3. Compare the responses (message text, status code, timing, error details)
4. Use Burp Intruder to test a list of candidate usernames
5. Identify valid usernames by the difference in responses

### Why It Works

The application returns different error messages for invalid usernames vs. invalid passwords. For example, 'Username not found' vs. 'Incorrect password'. This difference allows an attacker to determine which usernames exist in the system, which is useful for targeted brute-force attacks.

### Key Takeaways

- Return the same generic error for all login failures ('Invalid credentials')
- Do not reveal whether the username or password was wrong
- Implement consistent response timing
- Rate-limit login attempts to prevent enumeration
