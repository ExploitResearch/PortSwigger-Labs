# Reflected XSS into attribute with angle brackets HTML-encoded

**Lab URL:** https://portswigger.net/web-security/cross-site-scripting/contexts/lab-attribute-angle-brackets-html-encoded

## Metadata

| Property | Value |
|----------|-------|

---

### Target Goal - 

Exploit reflected XSS vulnerability to call the alert function

### Analysis/Exploitation

we use`"` to close string in value and then our script but we can observe that angular bracket get encoded

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/images/39af0f36d9b8_001.png)

so we are going to use event handler

```javascript
"onmouseover="alert(1)
```

the first `"` is used to close string in value so we come out of value 

we don’t use `"` at the end of alert because previous `"` from value will close it

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/images/39af0f36d9b8_002.png)
