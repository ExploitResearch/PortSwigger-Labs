# DOM-based open redirection

### Goal -

Solve the PortSwigger lab: DOM-based open redirection

### Exploitation

1. Identify the vulnerability type and injection point
2. Craft the appropriate payload
3. Deliver the payload and verify the result

### Why It Works

The exploit succeeds because this lab contains a dom-based open-redirection vulnerability. to solve this lab, exploit this vulnerability and redirect the victim to the exploit server.

The official solution confirms: The blog post page contains the following link, which returns to the home page of the blog: &lt;a href='#' onclick='returnURL' = /url=https?:\/\/.+)/.

The root cause is a failure in the application's security architecture specific to this dom based scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- This lab contains DOM-based open-redirection vulnerability, demonstrating how dom based vulnerabilities manifest in real applications.
- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab contains a DOM-based open-redirection vulnerability. To solve this lab, exploit this vulner"
- Server-side validation and authorization are the primary defenses.

## PortSwigger Lab

**Official lab:** DOM-based open redirection

**PortSwigger:** https://portswigger.net/web-security/dom-based/open-redirection/lab-dom-open-redirection
