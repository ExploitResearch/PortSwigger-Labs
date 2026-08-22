# Clickjacking with a frame buster script

### Goal -

Bypass a frame-busting JavaScript to perform a clickjacking attack.

### Vulnerability / Concept

The application uses a JavaScript frame-busting script that checks if the page is framed and redirects if so. However, the script can be bypassed using the `sandbox` attribute on the iframe.

### Exploitation

1. Verify the page has a frame-busting script (check source code)
2. Create an iframe with `sandbox='allow-scripts allow-forms'` (without `allow-top-navigation`)
3. The sandbox prevents the frame-buster from redirecting the top window
4. Overlay deceptive UI elements on the framed page

### Why It Works

The frame-buster script calls `top.location = self.location` to break out of frames. The `sandbox` attribute without `allow-top-navigation` prevents the script from modifying the top-level navigation, effectively neutralizing the frame-buster while still allowing scripts to run.

### Key Takeaways

- Frame-busting scripts can be bypassed with iframe sandbox attributes
- Use `X-Frame-Options` or CSP `frame-ancestors` instead of JavaScript
- Server-side headers cannot be bypassed by client-side techniques
- Defense in depth: use both headers and JavaScript
