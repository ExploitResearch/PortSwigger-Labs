# Using PHAR deserialization to deploy a custom gadget chain

### Goal -

Solve the PortSwigger lab: Using PHAR deserialization to deploy a custom gadget chain

### Exploitation

1. Identify the serialization format (PHP, Java, Ruby, Python, .NET)
2. Decode and modify the serialized object to change properties
3. Re-encode and submit the modified serialized data
4. For RCE: research and use known gadget chains for the target framework

### Why It Works

The exploit succeeds because this lab does not explicitly use deserialization. however, if you combine phar deserialization with other advanced hacking techniques, you can still achieve remote code execution via a custom gadget c

The official solution confirms: Observe that the website has a feature for uploading your own avatar, which only accepts JPG images. Upload a valid JPG as your avatar. Notice that it

The root cause is a failure in the application's security architecture specific to this deserialization scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab does not explicitly use deserialization. However, if you combine PHAR deserialization with "
- Never deserialize untrusted data — use JSON with allowlists instead.
