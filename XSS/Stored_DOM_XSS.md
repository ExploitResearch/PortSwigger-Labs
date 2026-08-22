# Stored DOM XSS

**Lab URL:** https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-dom-xss-stored

## Metadata

| Property | Value |
|----------|-------|

---

### Target Goal 

### Analysis/Exploitation:

### analysing code

**In line 5, the **`comments`** variable is parsing an JSON object:**

```javascript
let comments = JSON.parse(this.responseText);
```

**Then in line 12-14, we can see that it’s escaping HTML code:**

```javascript
function escapeHTML(html) {
    return html.replace('<', '&lt;').replace('>', '&gt;');
}
```

**The **`<`** and **`>`** will be replaced as **`&lt;`** and **`&gt;`**.**

We also see that the JavaScript file uses `innerHTML` in `comment.author`, `comment.body`, which is a sink (Dangerous function).

`let newInnerHtml = firstPElement.innerHTML + escapeHTML(comment.author)`

Armed with above information, we can start to bypass the `<>` HTML encoding.

According to W3School, **the **`replace()`** method only replace the first instance.**

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/images/56f22be1a806_001.png)

Which means if we add more than 1 `<` or `>`, it’ll be ignored.

**Let’s craft the XSS payload:**

```javascript
<><img src=errorpls onerror=alert(document.domain)>

```

### Why It Works

This lab demonstrates a stored DOM vulnerability in the blog comment functionality.

### Key Takeaways

- This lab demonstrates a stored DOM vulnerability in the blog comment functionality.
