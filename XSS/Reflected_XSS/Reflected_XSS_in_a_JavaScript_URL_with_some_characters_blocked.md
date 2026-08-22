# Reflected XSS in a JavaScript URL with some characters blocked

### Goal -

Perform a reflected XSS attack via a JavaScript URL when certain characters are blocked by the application.

### Exploitation

1. Identify that input is reflected in a JavaScript URL context (href="javascript:...")
2. Test which characters are blocked (quotes, angle brackets, etc.)
3. Use alternative encoding or characters that achieve the same result
4. Craft a payload using HTML entities, Unicode, or template literals

### Why It Works

The exploit succeeds because this lab reflects your input in a javascript url, but all is not as it seems. this initially seems like a trivial challenge; however, the application is blocking some characters in an attempt to preve

The official solution confirms: Visit the following URL, replacing YOUR-LAB-ID with your lab ID: https://YOUR-LAB-ID.web-security-academy.net/post?postId=5&amp;%27},x=x=%3E{throw/**/

The root cause is a failure in the application's security architecture specific to this cross site scripting scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab reflects your input in a JavaScript URL, but all is not as it seems. This initially seems l"
- Context-aware output encoding is the primary defense — the correct encoding depends on where input is reflected.

## PortSwigger Lab

**Official lab:** Reflected XSS in a JavaScript URL with some characters blocked

**PortSwigger:** https://portswigger.net/web-security/cross-site-scripting/contexts/lab-javascript-url-some-characters-blocked
