# DOM XSS in jQuery anchor href attribute sink using location.search source

**Lab URL:** https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-jquery-href-attribute-sink

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

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/images/97583e590fc1_001.png)
