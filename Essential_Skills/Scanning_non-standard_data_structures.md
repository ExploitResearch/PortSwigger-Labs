# Scanning non-standard data structures

### Goal -

Solve the PortSwigger lab: Scanning non-standard data structures

### Exploitation

1. Configure Burp Scanner for the target data structure
2. Run targeted scans on identified insertion points
3. Analyze scanner findings and verify manually

### Why It Works

The exploit succeeds because this lab contains a vulnerability that is difficult to find manually. it is located in a non-standard data structure.

The official solution confirms: Identify the vulnerability Log in to your account with the provided credentials. In Burp, go to the Proxy &gt; HTTP history tab.

The root cause is a failure in the application's security architecture specific to this essential skills scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- This lab contains vulnerability that is difficult to find manually, demonstrating how essential skills vulnerabilities manifest in real applications.
- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab contains a vulnerability that is difficult to find manually. It is located in a non-standar"
- Server-side validation and authorization are the primary defenses.

## PortSwigger Lab

**Official lab:** Scanning non-standard data structures

**PortSwigger:** https://portswigger.net/web-security/essential-skills/using-burp-scanner-during-manual-testing/lab-scanning-non-standard-data-structures
