# Modifying serialized objects

**Lab URL:** https://portswigger.net/web-security/deserialization/exploiting/lab-deserialization-modifying-serialized-objects

### Goal -

Solve the PortSwigger lab: Modifying serialized objects

### Exploitation

1. Identify the serialization format (PHP, Java, Ruby, Python, .NET)
2. Decode and modify the serialized object to change properties
3. Re-encode and submit the modified serialized data
4. For RCE: research and use known gadget chains for the target framework
