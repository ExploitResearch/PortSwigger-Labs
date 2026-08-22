# SameSite Strict bypass via sibling domain

### Goal - 

Perform a cross-site websocket hijacking attack to exfiltrate the victim's chat history and compromise the victim's account.

### Analysis/Exploitation -

It uses WebSocket in the chat:

```html
var webSocket = new WebSocket(chatForm.getAttribute("action"));
```

We also see that function `sendMessage()` is calling function `htmlEncode()` to HTML encode our input:

```html
function htmlEncode(str) {
    if (chatForm.getAttribute("encode")) {
        return String(str).replace(/['"<>&\r\n\\]/gi, function (c) {
            var lookup = {'\\': '&#x5c;', '\r': '&#x0d;', '\n': '&#x0a;', '"': '&quot;', '<': '&lt;', '>': '&gt;', "'": '&#39;', '&': '&amp;'};
            return lookup[c];
        });
    }
    return str;
}
```

it HTML encodes many characters. So normal DOM-based XSS won’t exploitable.

However, since it’s using WebSocket to communicate the chat, **we can try to test CSWSH (Cross-Site WebSocket Hijacking).**

First, let’s send a test message, and intercept all WebSocket requests via Burp Suite:

In the above WebSocket requests, we can see that **it’s vulnerable to CSRF(Cross-Site Request Forgery), as there is no CSRF token or unpredictable values in request parameters.**

**Then, we can refresh the page:**

It’ll send a `READY` message to render all chat messages.

If the WebSocket handshake request is vulnerable to CSRF, then an 
attacker’s web page can perform a cross-site request to open a WebSocket
 on the vulnerable site!

**To do so, I’ll craft a HTML form that automatically send a WebSocket request to **`/chat`** with message **`READY`**, and exfiltrate the victim’s chat history:**

### Why It Works

The exploit succeeds because this lab's live chat feature is vulnerable to cross-site websocket hijacking (cswsh). to solve the lab, log in to the victim's account.

The root cause is a failure in the application's security architecture specific to this csrf scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab's live chat feature is vulnerable to cross-site WebSocket hijacking (CSWSH). To solve the l"
- CSRF tokens, SameSite cookies, and Referer validation together provide defense-in-depth.
