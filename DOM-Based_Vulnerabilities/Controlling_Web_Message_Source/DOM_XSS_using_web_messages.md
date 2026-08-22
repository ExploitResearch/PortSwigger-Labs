# DOM XSS using web messages

### Goal -

Solve the PortSwigger lab: DOM XSS using web messages

### Exploitation

1. Identify the vulnerability type and injection point
2. Craft the appropriate payload
3. Deliver the payload and verify the result

### Why It Works

The exploit succeeds because this lab uses web messaging and parses the message as json. to solve the lab, construct an html page on the exploit server that exploits this vulnerability and calls the print() function.

The official solution confirms: Notice that the home page contains an event listener that listens for a web message. This event listener expects a string that is parsed using JSON.pa

The root cause is a failure in the application's security architecture specific to this dom based scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab uses web messaging and parses the message as JSON. To solve the lab, construct an HTML page"
- Server-side validation and authorization are the primary defenses.

## PortSwigger Lab

**Official lab:** DOM XSS using web messages

**PortSwigger:** https://portswigger.net/web-security/dom-based/controlling-the-web-message-source/lab-dom-xss-using-web-messages
