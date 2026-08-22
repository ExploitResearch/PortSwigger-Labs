# Clickjacking with a frame buster script

**Lab URL:** https://portswigger.net/web-security/clickjacking/lab-frame-buster-script

### Goal -

Bypass a frame-busting JavaScript to perform a clickjacking attack.

### Exploitation

1. Verify the page has a frame-busting script (check source code)
2. Create an iframe with `sandbox='allow-scripts allow-forms'` (without `allow-top-navigation`)
3. The sandbox prevents the frame-buster from redirecting the top window
4. Overlay deceptive UI elements on the framed page

### Why It Works

This lab is protected by a frame buster which prevents the website from being framed.

### Key Takeaways

- This lab is protected by a frame buster which prevents the website from being framed.
