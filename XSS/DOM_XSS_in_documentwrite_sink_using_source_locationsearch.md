# DOM XSS in document.write sink using source location.search

## Metadata

| Property | Value |
|----------|-------|

---

### Target Goal 

Exploit the DOM-based XSS vulnerability to call the alert function.


### Vulnerability / Concept

Cross-Site Scripting (XSS) occurs when user-controlled input is reflected or stored in the web page without proper sanitization or encoding. The browser cannot distinguish between legitimate page content and attacker-injected scripts, so it executes the injected JavaScript in the context of the vulnerable application.

XSS has three main types: Reflected (input is immediately reflected in the response), Stored (input is persisted and rendered when other users view the page), and DOM-based (the vulnerability is in client-side JavaScript that processes untrusted data into a dangerous sink).

The attack surface includes search fields, comment sections, profile fields, URL parameters, HTTP headers, and any data that is rendered in the browser without proper context-aware output encoding.

### Recon / Initial Analysis

1. Identify all input points that are reflected in the HTML response (search bars, forms, URL parameters)
2. Test with benign markers (e.g., `abc123xyz`) to find exact reflection points
3. Determine the context: HTML body, attribute value, JavaScript string, URL, CSS
4. Test which characters are encoded (<, >, ", ', `) and which pass through
5. For DOM-based XSS: inspect JavaScript source for dangerous sinks (innerHTML, document.write, eval, location.href)
6. For stored XSS: test comment fields, profile names, file upload metadata
7. Check if CSP is present and what it allows
8. Identify if the application uses frameworks (Angular, React, Vue) that may have template injection

### Analysis/Exploitation:

When function `trackSearch(query)` is called, it will:

- Write an `<img>` tag to the page
- `query` = a new object that searches GET parameter `search`
Here the parameter `search` is directly concatenate to the variable `query`, without any escape, encoding, sanitization.

Hence, we can inject a sink(Dangerous JavaScript function) via DOM(Document Object Model), which will then trigger function `alert()`:

**"><script>alert()</script>**

Note: The `'">` is to close the `<img>` tag, so we can write any JavaScript code.

![](./images/91b2f043542e_001.png)

### Why It Works

The application outputs user-controlled data into the HTML response without context-appropriate encoding. The browser's HTML parser cannot distinguish between legitimate page elements and attacker-injected content, so it executes injected `<script>` tags or event handlers.

In DOM-based XSS, the vulnerability is entirely client-side: JavaScript reads from a source (location.hash, location.search, postMessage) and passes it to a sink (innerHTML, document.write, eval) without sanitization. The trust boundary is between the DOM source and the DOM sink.

### Real-World Impact

An attacker could:
- Steal session cookies and hijack user accounts (if HttpOnly is not set)
- Capture keystrokes (passwords, credit card numbers, messages)
- Perform actions on behalf of the victim (change email, transfer funds)
- Redirect users to phishing pages
- Deface the website
- Deliver malware via drive-by downloads
- Bypass CSRF protections by reading CSRF tokens from the DOM

### Remediation

- Use context-aware output encoding (HTML body, attribute, JavaScript string, URL — each has different encoding requirements)
- Use templating engines that auto-escape output (Jinja2 autoescape, Twig, React JSX)
- Implement Content Security Policy (CSP) with `script-src 'self'` and nonces
- Set `HttpOnly` and `Secure` flags on session cookies
- Sanitize HTML input with allowlist-based libraries (DOMPurify, bleach)
- For DOM-based XSS: use `textContent` instead of `innerHTML`, avoid `eval()` and `document.write()`

### Key Takeaways

- XSS is a context-dependent vulnerability — encoding must match the output context (HTML, attribute, JS, URL).
- Blocklists of dangerous tags/attributes always miss something — use allowlists or proper encoding.
- DOM-based XSS is entirely client-side — server-side encoding doesn't help; sanitize at the sink.
- CSP is defense-in-depth, not a replacement for output encoding.
- HttpOnly on cookies prevents cookie theft via XSS but not other XSS impacts (action hijacking, keylogging).
