# Scanning non-standard data structures

**Lab URL:** https://portswigger.net/web-security/essential-skills/using-burp-scanner-during-manual-testing/lab-scanning-non-standard-data-structures

### Goal -

Solve the PortSwigger lab: Scanning non-standard data structures

### Exploitation

1. Configure Burp Scanner for the target data structure
2. Run targeted scans on identified insertion points
3. Analyze scanner findings and verify manually

### Why It Works

The application has a a vulnerability in a non-standard data structure, which can be exploited by crafting input that bypasses the insufficient validation in place.

### Key Takeaways

- The a vulnerability is exploitable because user input is processed without adequate validation.
