# Modifying serialized objects

### Goal -

Solve the PortSwigger lab: Modifying serialized objects

### Exploitation

1. Identify the serialization format (PHP, Java, Ruby, Python, .NET)
2. Decode and modify the serialized object to change properties
3. Re-encode and submit the modified serialized data
4. For RCE: research and use known gadget chains for the target framework

### Why It Works

The exploit succeeds because this lab uses a serialization-based session mechanism and is vulnerable to privilege escalation as a result. to solve the lab, edit the serialized object in the session cookie to exploit this vulnerab

The official solution confirms: Log in using your own credentials. Notice that the post-login GET /my-account request contains a session cookie that appears to be URL and Base64-enco

The root cause is a failure in the application's security architecture specific to this deserialization scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab uses a serialization-based session mechanism and is vulnerable to privilege escalation as a"
- Never deserialize untrusted data — use JSON with allowlists instead.

## PortSwigger Lab

**Official lab:** Modifying serialized objects

**PortSwigger:** https://portswigger.net/web-security/deserialization/exploiting/lab-deserialization-modifying-serialized-objects
