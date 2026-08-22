# Prototype Pollution

Prototype pollution is a JavaScript vulnerability that allows attackers to inject properties into the prototype chain of objects. By polluting `Object.prototype` or other prototypes, an attacker can modify the behavior of all objects that inherit from that prototype, potentially leading to DOM XSS, privilege escalation, or remote code execution.

**Client-side prototype pollution** targets browser JavaScript and can lead to DOM XSS.
**Server-side prototype pollution** targets Node.js applications and can lead to RCE.

## Contents

- [Client-side prototype pollution via browser APIs](./Client-side_prototype_pollution_via_browser_APIs.md)
- [DOM XSS via client-side prototype pollution](./DOM_XSS_via_client-side_prototype_pollution.md)
- [DOM XSS via an alternative prototype pollution vector](./DOM_XSS_via_an_alternative_prototype_pollution_vector.md)
- [Client-side prototype pollution via flawed sanitization](./Client-side_prototype_pollution_via_flawed_sanitization.md)
- [Client-side prototype pollution in third-party libraries](./Client-side_prototype_pollution_in_third-party_libraries.md)
- [Privilege escalation via server-side prototype pollution](./Privilege_escalation_via_server-side_prototype_pollution.md)
- [Detecting server-side prototype pollution without polluted property reflection](./Detecting_server-side_prototype_pollution_without_polluted_property_reflection.md)
- [Bypassing flawed input filters for server-side prototype pollution](./Bypassing_flawed_input_filters_for_server-side_prototype_pollution.md)
- [Remote code execution via server-side prototype pollution](./Remote_code_execution_via_server-side_prototype_pollution.md)
- [Exfiltrating sensitive data via server-side prototype pollution](./Exfiltrating_sensitive_data_via_server-side_prototype_pollution.md)
