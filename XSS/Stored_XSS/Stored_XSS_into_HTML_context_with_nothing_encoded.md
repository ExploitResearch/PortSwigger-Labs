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

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/images/90072dedd134_001.png)

### Why It Works

The exploit succeeds because this lab contains a stored cross-site scripting vulnerability in the comment functionality.

The official solution confirms: Enter the following into the comment box: &lt;script&gt;alert(1)&lt;/script&gt; Enter a name, email and website. Click

The root cause is a failure in the application's security architecture specific to this cross site scripting scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- This lab contains stored cross-site scripting vulnerability, demonstrating how cross site scripting vulnerabilities manifest in real applications.
- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab contains a stored cross-site scripting vulnerability in the comment functionality."
- Context-aware output encoding is the primary defense — the correct encoding depends on where input is reflected.

## PortSwigger Lab

**Official lab:** Stored XSS into HTML context with nothing encoded

**PortSwigger:** https://portswigger.net/web-security/cross-site-scripting/stored/lab-html-context-nothing-encoded
