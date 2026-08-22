# Stored XSS into onclick event with angle brackets and double quotes HTML-encoded

### Goal -

Solve the PortSwigger lab: Stored XSS into onclick event with angle brackets and double quotes HTML-encoded

### Exploitation

1. Identify the vulnerability type and injection point
2. Craft the appropriate payload
3. Deliver the payload and verify the result

### Why It Works

The exploit succeeds because this lab contains a stored cross-site scripting vulnerability in the comment functionality.

The official solution confirms: Post a comment with a random alphanumeric string in the "Website" input, then use Burp Suite to intercept the request and send it to Burp Repeater. Ma

The root cause is a failure in the application's security architecture specific to this cross site scripting scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- This lab contains stored cross-site scripting vulnerability, demonstrating how cross site scripting vulnerabilities manifest in real applications.
- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab contains a stored cross-site scripting vulnerability in the comment functionality."
- Context-aware output encoding is the primary defense — the correct encoding depends on where input is reflected.

## PortSwigger Lab

**Official lab:** Stored XSS into onclick event with angle brackets and double quotes HTML-encoded and single quotes a

**PortSwigger:** https://portswigger.net/web-security/cross-site-scripting/contexts/lab-onclick-event-angle-brackets-double-quotes-html-encoded-single-quotes-backslash-escaped
