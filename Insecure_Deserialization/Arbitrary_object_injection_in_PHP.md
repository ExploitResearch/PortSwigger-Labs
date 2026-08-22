# Arbitrary object injection in PHP

**Lab URL:** https://portswigger.net/web-security/deserialization/exploiting/lab-deserialization-arbitrary-object-injection-in-php

### Goal -

Solve the PortSwigger lab: Arbitrary object injection in PHP

### Exploitation

1. Identify the serialization format (PHP, Java, Ruby, Python, .NET)
2. Decode and modify the serialized object to change properties
3. Re-encode and submit the modified serialized data
4. For RCE: research and use known gadget chains for the target framework
