# Reflected DOM XSS

**Lab URL:** https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-dom-xss-reflected

## Metadata

| Property | Value |
|----------|-------|

---

### Target Goal 

Exploit the DOM XSS vulnerability to call the alert function.

### Analysis/Exploitation:

```javascript
\"-alert(1)}// 
or
12345\"}; alert(1);//
```

In the first `\`, we want to escape the `\` that the server-side application added to `"`

we close the JSON object via `}`. Then, commented out `"}` via `//`.

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/images/c79ae1f47486_001.png)

### Why It Works

This lab demonstrates a reflected DOM vulnerability.

### Key Takeaways

- This lab demonstrates a reflected DOM vulnerability.
