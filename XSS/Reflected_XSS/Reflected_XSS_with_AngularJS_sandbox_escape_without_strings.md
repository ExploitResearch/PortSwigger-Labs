# Reflected XSS with AngularJS sandbox escape without strings

### Goal -

Perform a cross-site scripting attack that breaks out of the AngularJS sandbox and executes JavaScript without using the string type.

### Vulnerability / Concept

The application uses AngularJS and has a reflected XSS vulnerability. The AngularJS sandbox restricts access to potentially dangerous functions. However, the sandbox can be escaped using prototype chain manipulation.

### Exploitation

1. Identify the AngularJS sandbox by testing if standard JavaScript functions are blocked
2. Research AngularJS sandbox escape techniques that don't use strings
3. Craft a payload using AngularJS expression syntax: `{{$on.constructor('alert(1)')()}}` or similar
4. Deliver the payload via the vulnerable parameter

### Why It Works

The AngularJS sandbox evaluates expressions but can be escaped by accessing constructor properties through the prototype chain. By calling `$on.constructor`, an attacker can access the `Function` constructor and execute arbitrary code.

### Key Takeaways

- AngularJS sandbox is not a security boundary
- Update to Angular 2+ which removed sandboxing
- Use CSP to restrict script execution
- Sanitize all user input
