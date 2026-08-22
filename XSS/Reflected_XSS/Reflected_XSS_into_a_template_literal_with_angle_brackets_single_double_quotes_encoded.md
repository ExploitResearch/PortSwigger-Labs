# Reflected XSS into a template literal with angle brackets, single, double quotes encoded

**Lab URL:** https://portswigger.net/web-security/cross-site-scripting/contexts/lab-javascript-template-literal-angle-brackets-single-double-quotes-backslash-backticks-escaped

### Goal -

Perform a reflected XSS attack when the input is reflected inside a JavaScript template literal and angle brackets, single quotes, and double quotes are all encoded.

### Exploitation

1. Identify that input is reflected inside backticks (template literal)
2. Test if backticks are encoded (they likely aren't)
3. Break out of the template literal using a backtick: `` `${alert(1)}` ``
4. Use the `${...}` expression syntax to execute JavaScript
