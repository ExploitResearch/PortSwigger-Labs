# Cross-site WebSocket hijacking

**Lab URL:** https://portswigger.net/web-security/websockets/cross-site-websocket-hijacking/lab

### Goal -

Solve the PortSwigger lab: Cross-site WebSocket hijacking

### Exploitation

1. For message injection: craft malicious WebSocket messages with payloads
2. For cross-site hijacking: create a malicious page that opens a WebSocket to the target
3. For handshake manipulation: modify headers in the initial HTTP upgrade request
