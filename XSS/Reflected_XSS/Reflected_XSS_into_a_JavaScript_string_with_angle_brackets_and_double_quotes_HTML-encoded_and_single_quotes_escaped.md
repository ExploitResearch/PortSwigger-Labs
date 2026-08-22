# Reflected XSS into a JavaScript string with angle brackets and double quotes HTML-encoded and single quotes escaped

### Goal -

Perform a reflected XSS attack when angle brackets, double quotes are HTML-encoded, and single quotes are escaped with backslash.

### Exploitation

1. Identify that input is reflected inside a JavaScript string with single quotes
2. Test that single quotes are escaped as `\'`
3. Inject a backslash before the escaped quote: `\\'`
4. The backslash escapes the backslash, leaving the quote unescaped
5. Break out of the string and inject JavaScript code

## PortSwigger Lab

**Official lab:** Reflected XSS into a JavaScript string with angle brackets HTML encoded

**PortSwigger:** https://portswigger.net/web-security/cross-site-scripting/contexts/lab-javascript-string-angle-brackets-html-encoded
