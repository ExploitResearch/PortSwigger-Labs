# Reflected XSS with AngularJS sandbox escape without strings

**Lab URL:** https://portswigger.net/web-security/cross-site-scripting/contexts/client-side-template-injection/lab-angular-sandbox-escape-without-strings

### Goal -

Perform a cross-site scripting attack that breaks out of the AngularJS sandbox and executes JavaScript without using the string type.

### Exploitation

1. Identify the AngularJS sandbox by testing if standard JavaScript functions are blocked
2. Research AngularJS sandbox escape techniques that don't use strings
3. Craft a payload using AngularJS expression syntax: `{{$on.constructor('alert(1)')()}}` or similar
4. Deliver the payload via the vulnerable parameter
