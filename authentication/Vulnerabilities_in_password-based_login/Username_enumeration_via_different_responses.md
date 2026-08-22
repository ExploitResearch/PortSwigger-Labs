# Username enumeration via different responses

### Goal -

Enumerate valid usernames by observing differences in the application's response to login attempts with valid vs. invalid usernames.

### Exploitation

1. Attempt login with a known valid username and an invalid password
2. Attempt login with a random invalid username and the same password
3. Compare the responses (message text, status code, timing, error details)
4. Use Burp Intruder to test a list of candidate usernames
5. Identify valid usernames by the difference in responses
