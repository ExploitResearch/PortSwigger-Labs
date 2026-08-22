# DOM XSS in document.write sink using source location.search

## Metadata

| Property | Value |
|----------|-------|

---

### Target Goal 

Exploit the DOM-based XSS vulnerability to call the alert function.

### Analysis/Exploitation:

When function `trackSearch(query)` is called, it will:

- Write an `<img>` tag to the page
- `query` = a new object that searches GET parameter `search`
Here the parameter `search` is directly concatenate to the variable `query`, without any escape, encoding, sanitization.

Hence, we can inject a sink(Dangerous JavaScript function) via DOM(Document Object Model), which will then trigger function `alert()`:

**"><script>alert()</script>**

Note: The `'">` is to close the `<img>` tag, so we can write any JavaScript code.

![](./images/91b2f043542e_001.png)
