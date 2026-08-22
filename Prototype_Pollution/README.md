# Prototype Pollution

Prototype pollution is a JavaScript vulnerability that allows attackers to inject properties into the prototype chain of objects. By polluting `Object.prototype` or other prototypes, an attacker can modify the behavior of all objects that inherit from that prototype, potentially leading to DOM XSS, privilege escalation, or remote code execution.

**Client-side prototype pollution** targets browser JavaScript and can lead to DOM XSS.
**Server-side prototype pollution** targets Node.js applications and can lead to RCE.
