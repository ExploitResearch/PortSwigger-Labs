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

## Labs

- [Reflected XSS in a JavaScript URL with some characters blocked](./Reflected_XSS_in_a_JavaScript_URL_with_some_characters_blocked.md)
- [Reflected XSS in canonical link tag](./Reflected_XSS_in_canonical_link_tag.md)
- [Reflected XSS into HTML context with all tags blocked except custom ones](./Reflected_XSS_into_HTML_context_with_all_tags_blocked_except_custom_ones.md)
- [Reflected XSS into HTML context with most tags and attributes blocked](./Reflected_XSS_into_HTML_context_with_most_tags_and_attributes_blocked.md)
- [Reflected XSS into HTML context with nothing encoded](./Reflected_XSS_into_HTML_context_with_nothing_encoded.md)
- [Reflected XSS into a JavaScript string with angle brackets HTML encoded](./Reflected_XSS_into_a_JavaScript_string_with_angle_brackets_HTML_encoded.md)
- [Reflected XSS into a JavaScript string with angle brackets and double quotes HTML-encoded and single quotes escaped](./Reflected_XSS_into_a_JavaScript_string_with_angle_brackets_and_double_quotes_HTML-encoded_and_single_quotes_escaped.md)
- [Reflected XSS into a JavaScript string with single quote and backslash escaped](./Reflected_XSS_into_a_JavaScript_string_with_single_quote_and_backslash_escaped.md)
- [Reflected XSS into a template literal with angle brackets single double quotes encoded](./Reflected_XSS_into_a_template_literal_with_angle_brackets_single_double_quotes_encoded.md)
- [Reflected XSS into attribute with angle brackets HTML-encoded](./Reflected_XSS_into_attribute_with_angle_brackets_HTML-encoded.md)
- [Reflected XSS protected by CSP with CSP bypass](./Reflected_XSS_protected_by_CSP_with_CSP_bypass.md)
- [Reflected XSS protected by very strict CSP with dangling markup attack](./Reflected_XSS_protected_by_very_strict_CSP_with_dangling_markup_attack.md)
- [Reflected XSS with AngularJS sandbox escape and CSP](./Reflected_XSS_with_AngularJS_sandbox_escape_and_CSP.md)
- [Reflected XSS with AngularJS sandbox escape without strings](./Reflected_XSS_with_AngularJS_sandbox_escape_without_strings.md)
- [Reflected XSS with event handlers and href attributes blocked](./Reflected_XSS_with_event_handlers_and_href_attributes_blocked.md)
- [Reflected XSS with some SVG markup allowed](./Reflected_XSS_with_some_SVG_markup_allowed.md)
- [summary payloads](./summary_payloads.md)
