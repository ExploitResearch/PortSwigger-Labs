# Blind XXE with out-of-band interaction

### Goal -

Solve the PortSwigger lab: Blind XXE with out-of-band interaction

### Exploitation

1. Identify the XML processing point
2. Craft an XML payload with an external entity definition
3. For file read: use `<!ENTITY xxe SYSTEM "file:///etc/passwd">`
4. For SSRF: use `<!ENTITY xxe SYSTEM "http://internal-service/">`
5. For blind XXE: use parameter entities and external DTD for OOB exfiltration

## PortSwigger Lab

**Official lab:** Blind XXE with out-of-band interaction

**PortSwigger:** https://portswigger.net/web-security/xxe/blind/lab-xxe-with-out-of-band-interaction
