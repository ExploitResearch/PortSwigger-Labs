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

### Why It Works

The exploit succeeds because this lab contains a dom-based cross-site scripting vulnerability in the stock checker functionality. it uses the javascript document.write function, which writes data out to the page. the document.wri

The official solution confirms: On the product pages, notice that the dangerous JavaScript extracts a storeId parameter from the location.search source. It then uses document.write t

The root cause is a failure in the application's security architecture specific to this cross site scripting scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- This lab contains DOM-based cross-site scripting vulnerability, demonstrating how cross site scripting vulnerabilities manifest in real applications.
- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab contains a DOM-based cross-site scripting vulnerability in the stock checker functionality."
- Context-aware output encoding is the primary defense — the correct encoding depends on where input is reflected.

## PortSwigger Lab

**Official lab:** DOM XSS in document.write sink using source location.search

**PortSwigger:** https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-document-write-sink
