# Clickjacking with form input data prefilled from a URL parameter

### Goal -

Exploit a clickjacking vulnerability where form fields can be prefilled from URL parameters, allowing the attacker to pre-fill malicious values.

### Exploitation

1. Identify URL parameters that pre-fill form fields
2. Create an iframe pointing to the target with pre-filled malicious values
3. Make the iframe transparent and overlay it on a deceptive page
4. The user clicks what they think is a benign button but actually submits the pre-filled form
