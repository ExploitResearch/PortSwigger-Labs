# Stored XSS

Stored Cross-Site Scripting (XSS) is a type of web security vulnerability where an attacker injects malicious scripts into a web application, and these scripts are then permanently stored and served to other users when they access particular pages or retrieve specific content. This type of XSS can have a more lasting impact compared to reflected XSS because the injected script is persistent and affects multiple users.
### **How it Works:**
1. **Attacker finds a vulnerability:** Exploitable features like comment sections, product reviews, or user profiles allow attackers to inject malicious scripts.
1. **Malicious script is stored:** The injected code gets saved on the server, becoming part of the website's content.
1. **Victims unknowingly execute the script:** Every user who visits the infected page unknowingly executes the stored script in their browser.
1. **Attacker gains control:** The script can steal data, redirect users, or perform other malicious actions, impacting all visitors.
**Example:**
Suppose a forum allows users to post comments without proper filtering. An attacker injects a script like this:
`<script>document.cookie = "sessionID=stolenValue";</script>`
Every user who views that comment has the script executed, unknowingly sending their stolen session ID to the attacker.
### Potential Impact:
- **Session Theft:** An attacker can steal session cookies or other sensitive information from users who inadvertently trigger the malicious script.
- **Defacement:** Stored XSS can be used to deface websites by injecting content that alters the appearance or functionality of the site.
- **Malicious Actions:** An attacker can perform actions on behalf of the user, such as changing account settings, initiating financial transactions, or manipulating data.
### Mitigation Strategies for Stored XSS:
1. **Input Validation and Sanitization:**
  - Validate and sanitize user inputs before storing them. Ensure that user-generated content does not contain executable scripts.
1. **Output Encoding:**
  - Encode or escape user inputs when rendering them in HTML. This prevents the execution of embedded scripts.
1. **Content Security Policy (CSP):**
  - Implement Content Security Policy headers to restrict the types of content that a browser can execute. This helps mitigate the impact of XSS attacks.

## Labs

- [Stored XSS into HTML context with nothing encoded](./Stored_XSS_into_HTML_context_with_nothing_encoded.md)
- [Stored XSS into anchor href attribute with double quotes HTML-encoded](./Stored_XSS_into_anchor_href_attribute_with_double_quotes_HTML-encoded.md)
- [Stored XSS into onclick event with angle brackets and double quotes HTML-encoded](./Stored_XSS_into_onclick_event_with_angle_brackets_and_double_quotes_HTML-encoded.md)
