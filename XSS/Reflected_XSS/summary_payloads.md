# summary payloads


  1. **XSS between HTML tags**
    - **Nothing encoded**
```javascript
<script>alert(1)</script>
```

    - **Most tags and attributes blocked
** Find allowed tags by bruteforce using [XSS cheat sheet](https://portswigger.net/web-security/cross-site-scripting/cheat-sheet) ; then find allowed events
    - **All tags blocked except custom ones**
    - **Event handlers and href attributes blocked**
    - **Some SVG markup allowed**
  1. **XSS in HTML tag attributes**
    - **Angle brackets HTML-encoded**
use event handler

```javascript
"onmouseover="alert(1)
```

    - **canonical link tag**
  1. **XSS into JavaScript**
    - Terminating the existing script
      - **Single quote and backslash escaped**
    - Breaking out of a JavaScript string
      - **angle brackets HTML encoded**
use` ``;`` `to enter new line of javascript code or function

use` //` to comment rest of unnecessary/unuseful characters

use `‘ or “` to modify payload as required

```javascript
;alert(1);
```

      - **angle brackets and double quotes HTML-encoded and single quotes escaped**

> 💡 Inside Javascript directly use `print()` & `alert()`

