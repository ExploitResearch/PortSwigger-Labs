# Clobbering DOM attributes to bypass HTML filters

### Goal -

Solve the PortSwigger lab: Clobbering DOM attributes to bypass HTML filters

### Exploitation

1. Identify the vulnerability type and injection point
2. Craft the appropriate payload
3. Deliver the payload and verify the result

### Why It Works

The exploit succeeds because this lab uses the htmljanitor library, which is vulnerable to dom clobbering. to solve this lab, construct a vector that bypasses the filter and uses dom clobbering to inject a vector that calls the p

The official solution confirms: Go to one of the blog posts and create a comment containing the following HTML: &lt;form id=x tabindex=0 onfocus=print()&gt;&lt;input id=attributes&gt

The root cause is a failure in the application's security architecture specific to this dom based scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab uses the HTMLJanitor library, which is vulnerable to DOM clobbering. To solve this lab, con"
- Server-side validation and authorization are the primary defenses.

## PortSwigger Lab

**Official lab:** Clobbering DOM attributes to bypass HTML filters

**PortSwigger:** https://portswigger.net/web-security/dom-based/dom-clobbering/lab-dom-clobbering-attributes-to-bypass-html-filters
