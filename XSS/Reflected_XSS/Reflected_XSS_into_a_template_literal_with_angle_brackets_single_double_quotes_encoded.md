# Reflected XSS into a template literal with angle brackets, single, double quotes encoded

### Goal -

Perform a reflected XSS attack when the input is reflected inside a JavaScript template literal and angle brackets, single quotes, and double quotes are all encoded.

### Exploitation

1. Identify that input is reflected inside backticks (template literal)
2. Test if backticks are encoded (they likely aren't)
3. Break out of the template literal using a backtick: `` `${alert(1)}` ``
4. Use the `${...}` expression syntax to execute JavaScript

### Why It Works

The exploit succeeds because this lab contains a reflected cross-site scripting vulnerability in the search blog functionality. the reflection occurs inside a template string with angle brackets, single, and double quotes html en

The official solution confirms: Submit a random alphanumeric string in the search box, then use Burp Suite to intercept the search request and send it to Burp Repeater. Observe that 

The root cause is a failure in the application's security architecture specific to this cross site scripting scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- This lab contains reflected cross-site scripting vulnerability, demonstrating how cross site scripting vulnerabilities manifest in real applications.
- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab contains a reflected cross-site scripting vulnerability in the search blog functionality. T"
- Context-aware output encoding is the primary defense — the correct encoding depends on where input is reflected.

## PortSwigger Lab

**Official lab:** Reflected XSS into a template literal with angle brackets, single, double quotes, backslash and back

**PortSwigger:** https://portswigger.net/web-security/cross-site-scripting/contexts/lab-javascript-template-literal-angle-brackets-single-double-quotes-backslash-backticks-escaped
