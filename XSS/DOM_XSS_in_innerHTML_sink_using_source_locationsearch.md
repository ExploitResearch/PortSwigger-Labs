# DOM XSS in innerHTML sink using source location.search

## Metadata

| Property | Value |
|----------|-------|

---

To inject `alert()` JavaScript function, we first need to know that `innerHTML`** sink doesn’t accept **`script`** elements** on any modern browser.**In order do trigger an **`alert()`**, we need to use event handler. Such as **`onerror`**:**

```html
<img src=1 onerror=alert(1)>
```

The value of the `src` attribute is invalid and throws an error. This triggers the `onerror` event handler, which then calls the `alert()`

### Why It Works

The exploit succeeds because this lab contains a dom-based cross-site scripting vulnerability in the search blog functionality. it uses an innerhtml assignment, which changes the html contents of a div element, using data from lo

The official solution confirms: Enter the following into the into the search box: &lt;img src=1 onerror=alert(1)&gt; Click "Search". The value

The root cause is a failure in the application's security architecture specific to this cross site scripting scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- This lab contains DOM-based cross-site scripting vulnerability, demonstrating how cross site scripting vulnerabilities manifest in real applications.
- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab contains a DOM-based cross-site scripting vulnerability in the search blog functionality. I"
- Context-aware output encoding is the primary defense — the correct encoding depends on where input is reflected.
