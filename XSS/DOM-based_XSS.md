# DOM-based XSS

### DOM

The DOM is an internal data structure that stores all of the objects and properties of a web page. For example, every tag used in HTML code represents a DOM object. Additionally, the DOM of a web page contains information about such properties as the page URL and meta information. Developers may refer to these objects and properties using JavaScript and change them dynamically.

The Document Object Model is what makes dynamic, single-page applications possible. However, it is also what makes DOM-based cross-site scripting possible.

### DOM Based XSS

A DOM-based XSS attack is possible if the web application writes data to the Document Object Model without proper sanitization. The attacker can manipulate this data to include XSS content on the web page, for example, malicious JavaScript code.

{% hint style="info" %}
💡 Reflected and Stored XSS are server side injection issues while DOM based XSS is a client (browser) side injection issue.
{% endhint %}


## Sources and sinks in DOM-based cross-site scripting

Every DOM-based XSS vulnerability has two elements: the source of user input and the target where this user input is written, called a sink. Popular sources that attackers can manipulate are `document.URL`, `document.documentURI`, `location.href`, `location.search`, `location.*`, `window.name`, and `document.referrer`. 
Popular sinks are `document.write`,`(element).innerHTML`, `eval`, `setTimeout`, `setInterval`, and `execScript`. Note that this list is not exhaustive and many other sources and sinks also exist.

For JavaScript code to be vulnerable to DOM-based XSS, it must take information from a source that can be controlled by the attacker and then pass this information to a sink.

{% hint style="info" %}
**Using the above example, we can observe that:**

- The HTML page is static and there are no malicious scripts embedded into the page source code, as in the case of other types of XSS attacks.
That is, the page itself (the HTTP response that is) does not change, but the client side code contained in the page executes differently due to the malicious modifications that have occurred in the DOM environment.
- The script code never reaches the server if we use the # character. It is seen as a fragment and the browser does not forward it. Therefore, server-side attack detection tools will fail to detect this attack.
Note that in some cases, depending on the type of the URL, the payload might get to the server and it may be impossible to hide it.
{% endhint %}

### **Impact:**

- **Data theft:** Attackers can steal sensitive information like cookies, session tokens, or form data.
- **Account takeover:** They can hijack user accounts or redirect victims to phishing pages.
- **Spreading malware:** Downloaded scripts can further compromise systems or launch additional attacks.
- **Disruption and annoyance:** Malicious code can alter website content, display unwanted messages, or redirect users to malicious websites.

### **Prevention:**

- **Client-side input validation and sanitization:** Validate and sanitize all user input and data sources before using them in the DOM to prevent code injection.
- **Content Security Policy (CSP):** Restrict sources allowed to execute scripts, preventing unauthorized code from running.
- **DOMPurify or similar libraries:** Utilize libraries that safely parse and sanitize HTML content before injecting it into the DOM.
- **Regular security updates:** Patch vulnerabilities in JavaScript libraries and frameworks promptly.

**[New database]** (database)

### Why It Works

The vulnerability exists because the application processes user-controlled input without adequate security validation. In this specific lab, the attack succeeds because:

- The application trusts the user input without proper server-side validation
- The input reaches a sensitive operation (database query, HTML rendering, system command, etc.) without sanitization
- The security boundary that should protect the operation is missing or incorrectly implemented
- The specific payload used exploits the exact weakness in the application's input handling

The PortSwigger lab description confirms this: "This lab contains an XSS vulnerability that is triggered by a click. Construct a clickjacking attack that fools the user into clicking the "Click me" button to call the print() function."

### Attack Flow

**Attack Flow:**

```
Attacker Input (payload in request)
        ↓
Application Functionality (processes user input)
        ↓
Server Processing (no validation/sanitization)
        ↓
Injection Point (input reaches sensitive operation)
        ↓
Exploitation (payload executes as intended)
        ↓
Lab Objective Achieved
```

### Real-World Impact

An attacker could trick users into performing actions they didn't intend (delete account, change email, transfer funds), capture keystrokes, trigger DOM-based XSS, or perform multi-step clickjacking attacks.

### Detection / Testing Methodology

1. Check if the target page can be framed (no X-Frame-Options or frame-ancestors CSP)
2. Verify if the page has JavaScript frame-busting (and test bypass via sandbox attribute)
3. Check if form fields can be pre-filled from URL parameters
4. Identify state-changing actions that could be clickjacked
5. Test if the page can be chained with DOM-based XSS

### Remediation

- Set X-Frame-Options: DENY or SAMEORIGIN
- Use CSP frame-ancestors 'none' or 'self'
- Do not rely on JavaScript frame-busting scripts (they can be bypassed)
- Implement both headers and JavaScript for defense-in-depth
- Do not allow form pre-filling from URL parameters for sensitive forms

### Key Takeaways

- This lab demonstrates a clickjacking vulnerability in a real-world scenario.
- The vulnerability occurs because user input reaches a sensitive operation without proper validation.
- The PortSwigger lab confirms: "This lab contains an XSS vulnerability that is triggered by a click. Construct a clickjacking attack"
- Burp Suite is essential for identifying and exploiting this vulnerability.
- The remediation for this specific vulnerability involves: - Set X-Frame-Options: DENY or SAMEORIGIN
