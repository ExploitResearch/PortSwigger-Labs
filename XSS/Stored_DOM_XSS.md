# Stored DOM XSS

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

The exploit succeeds because this lab demonstrates a stored dom vulnerability in the blog comment functionality. to solve this lab, exploit this vulnerability to call the alert() function.

The official solution confirms: Post a comment containing the following vector: &lt;&gt;&lt;img src=1 onerror=alert(1)&gt; In an attempt to prevent XSS, the website uses the JavaScri

The root cause is a failure in the application's security architecture specific to this cross site scripting scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab demonstrates a stored DOM vulnerability in the blog comment functionality. To solve this la"
- Context-aware output encoding is the primary defense — the correct encoding depends on where input is reflected.

## PortSwigger Lab

**Official lab:** Stored DOM XSS

**PortSwigger:** https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-dom-xss-stored
