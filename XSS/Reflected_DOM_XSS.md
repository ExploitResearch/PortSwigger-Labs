# Reflected DOM XSS

## Metadata

| Property | Value |
|----------|-------|

---

### Target Goal 

Exploit the DOM XSS vulnerability to call the alert function.

### Analysis/Exploitation:

```javascript
\"-alert(1)}// 
or
12345\"}; alert(1);//
```

In the first `\`, we want to escape the `\` that the server-side application added to `"`

we close the JSON object via `}`. Then, commented out `"}` via `//`.

![](./images/c79ae1f47486_001.png)

### Why It Works

The exploit succeeds because this lab demonstrates a reflected dom vulnerability. reflected dom vulnerabilities occur when the server-side application processes data from a request and echoes the data in the response. a script on

The official solution confirms: In Burp Suite, go to the Proxy tool and make sure that the Intercept feature is switched on. Back in the lab, go to the target website and use the sea

The root cause is a failure in the application's security architecture specific to this cross site scripting scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab demonstrates a reflected DOM vulnerability. Reflected DOM vulnerabilities occur when the se"
- Context-aware output encoding is the primary defense — the correct encoding depends on where input is reflected.
