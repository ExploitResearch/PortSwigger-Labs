# Cross-site WebSocket hijacking

### Goal -

Solve the PortSwigger lab: Cross-site WebSocket hijacking

### Exploitation

1. For message injection: craft malicious WebSocket messages with payloads
2. For cross-site hijacking: create a malicious page that opens a WebSocket to the target
3. For handshake manipulation: modify headers in the initial HTTP upgrade request


### Why It Works

The exploit succeeds because to solve the lab, use the exploit server to host an html/javascript payload that uses a cross-site websocket hijacking attack to exfiltrate the victim's chat history, then use this gain access to thei

The official solution confirms: Click "Live chat" and send a chat message. Reload the page. In Burp Proxy, in the WebSockets history tab, observe that the "READY" command retrieves p

The root cause is a failure in the application's security architecture specific to this websockets scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- The PortSwigger lab description confirms: "To solve the lab, use the exploit server to host an HTML/JavaScript payload that uses a cross-site W"
- Validate WebSocket message origin and sanitize all messages.

## PortSwigger Lab

**Official lab:** Cross-site WebSocket hijacking

**PortSwigger:** https://portswigger.net/web-security/websockets/cross-site-websocket-hijacking/lab
