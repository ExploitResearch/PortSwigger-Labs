# DOM XSS in innerHTML sink using source location.search

**Lab URL:** https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-innerhtml-sink

## Metadata

| Property | Value |
|----------|-------|

---

To inject `alert()` JavaScript function, we first need to know that `innerHTML`** sink doesn’t accept **`script`** elements** on any modern browser.**In order do trigger an **`alert()`**, we need to use event handler. Such as **`onerror`**:**

```html
<img src=1 onerror=alert(1)>
```

The value of the `src` attribute is invalid and throws an error. This triggers the `onerror` event handler, which then calls the `alert()`
