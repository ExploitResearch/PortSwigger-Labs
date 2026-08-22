# Stored XSS into anchor href attribute with double quotes HTML-encoded

## Metadata

| Property | Value |
|----------|-------|

---

### Target Goal - 

Exploit stored XSS vulnerability to call the alert function

### Analysyis/Exploitation

![](./images/99de67491d5b_001.png)

![](./images/99de67491d5b_002.png)

after posting comment we can see that the url which we put in  website section is appearing in href 

instead of url we can insert script here

I tried to insert 

```javascript
<script>alert(1)</script>
"<script>alert(1)</script>
```

and when i clicked on comment they just get append at the end of our lab url and script didn’t work

![](./images/99de67491d5b_003.png)

### How to call javascript from a href

```javascript
<a href="#" onclick="myFunction()" >LinkText</a>
or
<a href="javascript:call_func();">...</a>
```

We can't use first one because double quotes are encode so we use 2nd method

```javascript
javascript:alert(1)
```

### Why It Works

The exploit succeeds because this lab contains a stored cross-site scripting vulnerability in the comment functionality. to solve this lab, submit a comment that calls the alert function when the comment author name is clicked.

The official solution confirms: Post a comment with a random alphanumeric string in the "Website" input, then use Burp Suite to intercept the request and send it to Burp Repeater. Ma

The root cause is a failure in the application's security architecture specific to this cross site scripting scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- This lab contains stored cross-site scripting vulnerability, demonstrating how cross site scripting vulnerabilities manifest in real applications.
- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab contains a stored cross-site scripting vulnerability in the comment functionality. To solve"
- Context-aware output encoding is the primary defense — the correct encoding depends on where input is reflected.

## PortSwigger Lab

**Official lab:** Stored XSS into anchor href attribute with double quotes HTML-encoded

**PortSwigger:** https://portswigger.net/web-security/cross-site-scripting/contexts/lab-href-attribute-double-quotes-html-encoded
