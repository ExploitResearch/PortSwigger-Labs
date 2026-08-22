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

### Why It Works

The application has a stored cross-site scripting vulnerability in comment functionality, which can be exploited by crafting input that bypasses the insufficient validation in place.

### Key Takeaways

- The stored cross-site scripting vulnerability is exploitable because user input is processed without adequate validation.
