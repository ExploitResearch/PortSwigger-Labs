# Reflected XSS

Reflected XSS (Cross-Site Scripting) is a type of web security vulnerability where malicious code is injected into a user's request and reflected back to them by the server, often without proper sanitization. This allows attackers to execute arbitrary code in the victim's browser, potentially leading to:

- **Stealing sensitive information:** Cookies, session tokens, and other data can be captured and misused.
- **Taking control of accounts:** Attackers can hijack user sessions or redirect them to malicious websites.
The vulnerability does not directly affect the web server or the database, it may very easily lead to severe consequences and further attacks.

### **How it Works:**

1. **Attacker crafts a malicious link or form:** This link or form contains the payload, usually hidden within URL parameters or form data.
  - **Spreading malware:** Malicious scripts can be injected to further compromise systems.
1. **Victim clicks the link or submits the form:** The payload is sent to the vulnerable server.
1. **Server processes the request:** The server, lacking proper validation, incorporates the payload into the response.
1. **Victim's browser executes the script:** The response reaches the victim's browser, which unknowingly executes the malicious code due to trust in the server.
**Example:**

Imagine a search bar on a website vulnerable to reflected XSS. An attacker might create a link like this:

`https://example.com/search?q=<script>alert('XSS attack!')</script>`

When a victim clicks this link, the script embedded in the query parameter gets reflected back and executed in their browser, displaying an alert message.

### Impact of reflected XSS attacks

If an attacker can control a script that is executed in the victim's browser, then they can typically fully compromise that user. Amongst other things, the attacker can:

- Perform any action within the application that the user can perform.
- View any information that the user is able to view.
- Modify any information that the user is able to modify.
- Initiate interactions with other application users, including malicious attacks, that will appear to originate from the initial victim user.
### **Prevention:**

- **Server-side input validation and sanitization:** Ensure all user input is rigorously checked and sanitized to remove potentially harmful code before processing.
- **HttpOnly and Secure flags for cookies:** Mitigate cookie theft by setting these flags to prevent client-side access and transmission over unencrypted channels.
- **Content Security Policy (CSP):** Define trusted sources for scripts and other resources to restrict unauthorized execution.

**[New database]** (database)

## [summary payloads](./summary_payloads.md)

