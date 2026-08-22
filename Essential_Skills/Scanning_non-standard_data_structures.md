# Scanning non-standard data structures

### Goal -

Solve the PortSwigger lab: Scanning non-standard data structures

### Vulnerability / Concept

These labs test essential Burp Suite skills including targeted scanning, handling non-standard data structures, and identifying vulnerabilities efficiently using Burp's built-in scanner.

### Recon / Initial Analysis

1. Use Burp Suite's Scanner with targeted scanning modes
2. Identify non-standard data structures (JSON, XML, etc.) in requests
3. Configure Burp Scanner to test specific insertion points

### Exploitation

1. Configure Burp Scanner for the target data structure
2. Run targeted scans on identified insertion points
3. Analyze scanner findings and verify manually

### Why It Works

Burp Suite's scanner can identify many vulnerability types automatically, but it needs proper configuration for non-standard data structures. Understanding how to configure scanning is an essential skill for efficient security testing.

### Key Takeaways

- Configure Burp Scanner for the target application's data structures
- Use targeted scanning for efficiency
- Always verify scanner findings manually
- Understand Burp's insertion point configuration
