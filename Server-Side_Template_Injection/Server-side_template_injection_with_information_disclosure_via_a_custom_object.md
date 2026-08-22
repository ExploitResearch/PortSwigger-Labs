# Server-side template injection with information disclosure via a custom object

### Goal -

Solve the PortSwigger lab: Server-side template injection with information disclosure via a custom object

### Vulnerability / Concept

Server-side template injection occurs when user input is incorporated into a template string that is then rendered by a template engine. Instead of treating the input as data, the engine interprets it as template syntax, allowing code execution.

### Recon / Initial Analysis

1. Identify template rendering points (email templates, custom greetings, search results)
2. Test with template syntax probes: `{{7*7}}` (Jinja2/Twig), `<%= 7*7 %>` (ERB), `${7*7}` (FreeMarker)
3. Identify the template engine by testing engine-specific syntax
4. Check for sandbox restrictions that limit available functions

### Exploitation

1. Confirm SSTI by injecting template syntax that produces a mathematical result
2. Identify the template engine via fingerprinting payloads
3. Research the engine's documentation for dangerous functions and objects
4. Craft an exploit payload that accesses restricted objects or executes code

### Why It Works

The vulnerability exists because the application concatenates user input into a template string instead of passing it as a variable. Template engines like Jinja2, Twig, and FreeMarker evaluate expressions within `{{ }}` or `${ }` delimiters, so user input containing these delimiters is interpreted as template code.


### Real-World Impact

An attacker could:
- Execute arbitrary code on the server (remote code execution)
- Read sensitive files (configuration, credentials, source code)
- Access internal services and databases
- Modify or delete server-side data
- Pivot to other internal systems
- Achieve full server compromise


### Remediation

- Never concatenate user input into template strings; always use template variables
- Use sandboxed template environments with restricted function access
- Implement allowlists for template functions and filters
- Use logic-less templates (Mustache) where possible
- Validate and sanitize all template input
- Run template rendering in isolated containers or with restricted permissions

### Key Takeaways

- Never concatenate user input into template strings; always use template variables
- Use sandboxed template environments with restricted function access
- Input validation should reject template syntax characters
