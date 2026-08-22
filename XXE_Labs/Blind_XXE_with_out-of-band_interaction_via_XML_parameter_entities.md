# Blind XXE with out-of-band interaction via XML parameter entities

### Goal -

Solve the PortSwigger lab: Blind XXE with out-of-band interaction via XML parameter entities

### Exploitation

1. Identify the XML processing point
2. Craft an XML payload with an external entity definition
3. For file read: use `<!ENTITY xxe SYSTEM "file:///etc/passwd">`
4. For SSRF: use `<!ENTITY xxe SYSTEM "http://internal-service/">`
5. For blind XXE: use parameter entities and external DTD for OOB exfiltration

### Why It Works

The exploit succeeds because this lab has a "check stock" feature that parses xml input, but does not display any unexpected values, and blocks requests containing regular external entities.

The official solution confirms: Visit a product page, click "Check stock" and intercept the resulting POST request in Burp Suite Professional. Insert the following external entity de

The root cause is a failure in the application's security architecture specific to this xxe scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab has a "Check stock" feature that parses XML input, but does not display any unexpected valu"
- Disable external entity processing in XML parsers.

## PortSwigger Lab

**Official lab:** Blind XXE with out-of-band interaction via XML parameter entities

**PortSwigger:** https://portswigger.net/web-security/xxe/blind/lab-xxe-with-out-of-band-interaction-using-parameter-entities
