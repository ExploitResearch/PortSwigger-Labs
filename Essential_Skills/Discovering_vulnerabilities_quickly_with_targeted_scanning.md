# Discovering vulnerabilities quickly with targeted scanning

### Goal -

Solve the PortSwigger lab: Discovering vulnerabilities quickly with targeted scanning

### Exploitation

1. Configure Burp Scanner for the target data structure
2. Run targeted scans on identified insertion points
3. Analyze scanner findings and verify manually

### Why It Works

The exploit succeeds because this lab contains a vulnerability that enables you to read arbitrary files from the server. to solve the lab, retrieve the contents of /etc/passwd within 10 minutes.

The official solution confirms: This lab is designed to help you learn how targeted scans can assist you with basic recon. As such, we will not be providing a step-by-step solution.

The root cause is a failure in the application's security architecture specific to this essential skills scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- This lab contains vulnerability that enables you to read arbitrary files from the server, demonstrating how essential skills vulnerabilities manifest in real applications.
- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab contains a vulnerability that enables you to read arbitrary files from the server. To solve"
- Server-side validation and authorization are the primary defenses.
