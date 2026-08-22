# Reflected XSS into attribute with angle brackets HTML-encoded

## Metadata

| Property | Value |
|----------|-------|

---

### Target Goal - 

Exploit reflected XSS vulnerability to call the alert function

### Analysis/Exploitation

we use`"` to close string in value and then our script but we can observe that angular bracket get encoded

![](./images/39af0f36d9b8_001.png)

so we are going to use event handler

```javascript
"onmouseover="alert(1)
```

the first `"` is used to close string in value so we come out of value 

we don’t use `"` at the end of alert because previous `"` from value will close it

![](./images/39af0f36d9b8_002.png)

### Why It Works

The exploit succeeds because this lab contains a reflected cross-site scripting vulnerability in the search blog functionality where angle brackets are html-encoded. to solve this lab, perform a cross-site scripting attack that i

The official solution confirms: Submit a random alphanumeric string in the search box, then use Burp Suite to intercept the search request and send it to Burp Repeater. Observe that 

The root cause is a failure in the application's security architecture specific to this cross site scripting scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- This lab contains reflected cross-site scripting vulnerability, demonstrating how cross site scripting vulnerabilities manifest in real applications.
- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab contains a reflected cross-site scripting vulnerability in the search blog functionality wh"
- Context-aware output encoding is the primary defense — the correct encoding depends on where input is reflected.
