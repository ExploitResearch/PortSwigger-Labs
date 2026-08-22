# Modifying serialized objects

**Lab URL:** https://portswigger.net/web-security/deserialization/exploiting/lab-deserialization-modifying-serialized-objects

### Goal -

Solve the PortSwigger lab: Modifying serialized objects

### Exploitation

1. Identify the serialization format (PHP, Java, Ruby, Python, .NET)
2. Decode and modify the serialized object to change properties
3. Re-encode and submit the modified serialized data
4. For RCE: research and use known gadget chains for the target framework

### Why It Works

This lab uses a serialization-based session mechanism and is vulnerable to privilege escalation as a result.

### Key Takeaways

- The privilege escalation as a result. To solve the lab, edit the serialized object in the session cookie to exploit this vulnerability is exploitable because user input is processed without adequate validation.
