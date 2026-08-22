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

### Why It Works

The application has a simple reflected cross-site scripting vulnerability in search functionality, which can be exploited by crafting input that bypasses the insufficient validation in place.

### Key Takeaways

- The simple reflected cross-site scripting vulnerability is exploitable because user input is processed without adequate validation.
