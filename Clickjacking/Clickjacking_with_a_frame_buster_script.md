# Clickjacking with a frame buster script

### Goal -

Bypass a frame-busting JavaScript to perform a clickjacking attack.

### Exploitation

1. Verify the page has a frame-busting script (check source code)
2. Create an iframe with `sandbox='allow-scripts allow-forms'` (without `allow-top-navigation`)
3. The sandbox prevents the frame-buster from redirecting the top window
4. Overlay deceptive UI elements on the framed page

### Why It Works

The exploit succeeds because this lab is protected by a frame buster which prevents the website from being framed. can you get around the frame buster and conduct a clickjacking attack that changes the users email address?

The official solution confirms: Log in to the account on the target website. Go to the exploit server and paste the following HTML template into the "Body" section: &lt;style&gt; ifr

The root cause is a failure in the application's security architecture specific to this clickjacking scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab is protected by a frame buster which prevents the website from being framed. Can you get ar"
- Set X-Frame-Options or CSP frame-ancestors — JavaScript frame-busting is bypassable.
