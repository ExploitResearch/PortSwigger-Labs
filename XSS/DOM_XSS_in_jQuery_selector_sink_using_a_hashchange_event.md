# DOM XSS in jQuery selector sink using a hashchange event

## Metadata

| Property | Value |
|----------|-------|

---

### Target Goal:

Exploit the DOM-based XSS vulnerability to call the print() function

### Analysis/Exploit:

the `iframe`’s `src` attribute points to the vulnerable page with an empty hash value. When the `iframe` is loaded, an XSS payload is appended to the hash, causing the `hashchange` event to fire.

```javascript
<iframe src="https://0a63007904e71eb080612b3800ab000f.web-security-academy.net/#" onload="this.src+='<img src=x onError=print()>' "> </iframe>
```

![](./images/4b886ff1713c_001.png)

### Why It Works

The exploit succeeds because this lab contains a dom-based cross-site scripting vulnerability on the home page. it uses jquery's $() selector function to auto-scroll to a given post, whose title is passed via the location.hash pr

The official solution confirms: Notice the vulnerable code on the home page using Burp or the browser's DevTools. From the lab banner, open the exploit server. In the Body

The root cause is a failure in the application's security architecture specific to this cross site scripting scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- This lab contains DOM-based cross-site scripting vulnerability on the home page, demonstrating how cross site scripting vulnerabilities manifest in real applications.
- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab contains a DOM-based cross-site scripting vulnerability on the home page. It uses jQuery's "
- Context-aware output encoding is the primary defense — the correct encoding depends on where input is reflected.
