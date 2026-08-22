# Reflected XSS into HTML context with nothing encoded

**Lab URL:** https://portswigger.net/web-security/cross-site-scripting/reflected/lab-html-context-nothing-encoded

## Metadata

| Property | Value |
|----------|-------|

---

### Target Goal - 

Exploit XSS vulnerability to call the alert function.

### Analysis/Exploitation

**inject a JavaScript function called **`alert()`** in search function:**

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/images/2d7773f68e8a_001.png)
