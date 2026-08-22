# Clickjacking with form input data prefilled from a URL parameter

### Goal -

Exploit a clickjacking vulnerability where form fields can be prefilled from URL parameters, allowing the attacker to pre-fill malicious values.

### Vulnerability / Concept

The application allows form fields to be prefilled via URL parameters (e.g., `?email=attacker@evil.com`). Combined with the lack of frame-busting, this allows the attacker to pre-fill the form with malicious data and trick the user into submitting it.

### Exploitation

1. Identify URL parameters that pre-fill form fields
2. Create an iframe pointing to the target with pre-filled malicious values
3. Make the iframe transparent and overlay it on a deceptive page
4. The user clicks what they think is a benign button but actually submits the pre-filled form

### Why It Works

The application accepts URL parameters to pre-fill form data (a convenience feature). Combined with the lack of `X-Frame-Options`, the attacker can frame the page with pre-filled malicious values. The user's click submits the form with the attacker-controlled data.

### Key Takeaways

- Do not allow form pre-filling from URL parameters for sensitive forms
- Set `X-Frame-Options` or CSP `frame-ancestors`
- Validate form data server-side regardless of how it was entered
- Use CSRF tokens that are tied to the form's initial state
