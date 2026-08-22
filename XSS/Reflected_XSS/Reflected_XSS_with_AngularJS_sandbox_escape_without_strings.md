# Reflected XSS with AngularJS sandbox escape without strings

### Goal -

Perform a cross-site scripting attack that breaks out of the AngularJS sandbox and executes JavaScript without using the string type.

### Exploitation

1. Identify the AngularJS sandbox by testing if standard JavaScript functions are blocked
2. Research AngularJS sandbox escape techniques that don't use strings
3. Craft a payload using AngularJS expression syntax: `{{$on.constructor('alert(1)')()}}` or similar
4. Deliver the payload via the vulnerable parameter

### Why It Works

The exploit succeeds because to solve the lab, perform a cross-site scripting attack that bypasses csp, escapes the angularjs sandbox, and alerts document.cookie.

The official solution confirms: Go to the exploit server and paste the following code, replacing YOUR-LAB-ID with your lab ID: &lt;script&gt; location='https://YOUR-LAB-ID.web-securi

The root cause is a failure in the application's security architecture specific to this cross site scripting scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "To solve the lab, perform a cross-site scripting attack that bypasses CSP, escapes the AngularJS san"
- Context-aware output encoding is the primary defense — the correct encoding depends on where input is reflected.

## PortSwigger Lab

**Official lab:** Reflected XSS with AngularJS sandbox escape without strings

**PortSwigger:** https://portswigger.net/web-security/cross-site-scripting/contexts/client-side-template-injection/lab-angular-sandbox-escape-without-strings
