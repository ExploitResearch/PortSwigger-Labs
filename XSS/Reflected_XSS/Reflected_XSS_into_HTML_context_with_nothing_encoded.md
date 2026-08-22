# Reflected XSS into HTML context with nothing encoded

## Metadata

| Property | Value |
|----------|-------|

---

### Target Goal - 

Exploit XSS vulnerability to call the alert function.

### Analysis/Exploitation

**inject a JavaScript function called **`alert()`** in search function:**

![](./images/2d7773f68e8a_001.png)

### Why It Works

The exploit succeeds because to solve the lab, perform a cross-site scripting attack that injects a custom tag and automatically alerts document.cookie.

The official solution confirms: Go to the exploit server and paste the following code, replacing YOUR-LAB-ID with your lab ID: &lt;script&gt; location = 'https://YOUR-LAB-ID.web-secu

The root cause is a failure in the application's security architecture specific to this cross site scripting scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "To solve the lab, perform a cross-site scripting attack that injects a custom tag and automatically "
- Context-aware output encoding is the primary defense — the correct encoding depends on where input is reflected.
