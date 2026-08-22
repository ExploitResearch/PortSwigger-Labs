# Reflected XSS into a JavaScript string with angle brackets HTML encoded

## Metadata

| Property | Value |
|----------|-------|

---

'; → var searchTerms=**'';';**
 '; alert(1); →var searchTerms=**'; alert(1);';**
However, as seen, there is one ' character left unused. For this, I modified my payload to → **'; alert(1);' ** 

But if it still couldn’t trigger the XSS use a comment for the one ’ left  **'; alert(1);//'**

### Why It Works

The exploit succeeds because this lab contains a reflected cross-site scripting vulnerability in the search query tracking functionality where angle brackets and double are html encoded and single quotes are escaped.

The official solution confirms: Submit a random alphanumeric string in the search box, then use Burp Suite to intercept the search request and send it to Burp Repeater. Observe that 

The root cause is a failure in the application's security architecture specific to this cross site scripting scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- This lab contains reflected cross-site scripting vulnerability, demonstrating how cross site scripting vulnerabilities manifest in real applications.
- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab contains a reflected cross-site scripting vulnerability in the search query tracking functi"
- Context-aware output encoding is the primary defense — the correct encoding depends on where input is reflected.

## PortSwigger Lab

**Official lab:** Reflected XSS into a JavaScript string with angle brackets HTML encoded

**PortSwigger:** https://portswigger.net/web-security/cross-site-scripting/contexts/lab-javascript-string-angle-brackets-html-encoded
