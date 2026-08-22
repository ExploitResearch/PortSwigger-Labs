# Stored XSS into anchor href attribute with double quotes HTML-encoded

**Lab URL:** https://portswigger.net/web-security/cross-site-scripting/contexts/lab-href-attribute-double-quotes-html-encoded

## Metadata

| Property | Value |
|----------|-------|

---

### Target Goal - 

Exploit stored XSS vulnerability to call the alert function

### Analysyis/Exploitation

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/images/99de67491d5b_001.png)

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/images/99de67491d5b_002.png)

after posting comment we can see that the url which we put in  website section is appearing in href 

instead of url we can insert script here

I tried to insert 

```javascript
<script>alert(1)</script>
"<script>alert(1)</script>
```

and when i clicked on comment they just get append at the end of our lab url and script didn’t work

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/images/99de67491d5b_003.png)

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
