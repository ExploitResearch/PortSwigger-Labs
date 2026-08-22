# Server-Side Template Injection

Server-side template injection (SSTI) occurs when user input is embedded into server-side templates without proper sanitization. This allows attackers to inject template directives that execute arbitrary code on the server.

SSTI can affect any template engine: Jinja2 (Python), Twig (PHP), FreeMarker (Java), Velocity (Java), ERB (Ruby), and others. The impact ranges from information disclosure to full remote code execution.

## Labs

- [Basic server-side template injection](./Basic_server-side_template_injection.md)
- [Basic server-side template injection code context](./Basic_server-side_template_injection_code_context.md)
- [Server-side template injection in a sandboxed environment](./Server-side_template_injection_in_a_sandboxed_environment.md)
- [Server-side template injection in an unknown language with a documented exploit](./Server-side_template_injection_in_an_unknown_language_with_a_documented_exploit.md)
- [Server-side template injection using documentation](./Server-side_template_injection_using_documentation.md)
- [Server-side template injection with a custom exploit](./Server-side_template_injection_with_a_custom_exploit.md)
- [Server-side template injection with information disclosure via a custom object](./Server-side_template_injection_with_information_disclosure_via_a_custom_object.md)
