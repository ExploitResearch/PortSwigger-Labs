# DOM XSS in jQuery anchor href attribute sink using location.search source

## Metadata

| Property | Value |
|----------|-------|

---

we see **the form uses the jQuery library’s **`$`** selector function to find an anchor element, and changes its **`href`** attribute using data from **`location.search`**, which is the GET parameter **`returnPath`**.**

Now, in jQuery, **the **`attr()`** function can change the attributes of DOM elements.**

If data is read from a user-controlled source like the URL, then passed to the `attr()` function, then it may be possible to manipulate the value sent to cause XSS.

**To injection malicious JavaScript, we can change our **`returnPath`** GET parameter:**

The `returnPath` value likely corresponds to the `Back` link. Let’s try it out.

```javascript
javascript:alert(document.cookie)
```

![](./images/97583e590fc1_001.png)

### Why It Works

The exploit succeeds because this lab contains a dom-based cross-site scripting vulnerability in the submit feedback page. it uses the jquery library's $ selector function to find an anchor element, and changes its href attribute

The official solution confirms: On the Submit feedback page, change the query parameter returnPath to / followed by a random alphanumeric string. Right-click and inspect the element,

The root cause is a failure in the application's security architecture specific to this cross site scripting scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- This lab contains DOM-based cross-site scripting vulnerability, demonstrating how cross site scripting vulnerabilities manifest in real applications.
- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab contains a DOM-based cross-site scripting vulnerability in the submit feedback page. It use"
- Context-aware output encoding is the primary defense — the correct encoding depends on where input is reflected.

## PortSwigger Lab

**Official lab:** DOM XSS in jQuery anchor href attribute sink using location.search source

**PortSwigger:** https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-jquery-href-attribute-sink
