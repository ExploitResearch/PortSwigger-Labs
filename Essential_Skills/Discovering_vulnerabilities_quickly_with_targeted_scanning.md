# Discovering vulnerabilities quickly with targeted scanning

### Goal -

Solve the PortSwigger lab: Discovering vulnerabilities quickly with targeted scanning

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


### Real-World Impact

Proper use of Burp Suite Scanner enables:
- Rapid identification of vulnerabilities across large attack surfaces
- Detection of non-standard data structure vulnerabilities (JSON, XML, etc.)
- More efficient manual testing by automating repetitive scanning tasks
- Better coverage by testing insertion points that might be missed manually


### Remediation

- Configure Burp Scanner with appropriate insertion point types for the target application
- Use targeted scanning for specific data structures (JSON, XML, GraphQL)
- Set up crawl-and-scan workflows for comprehensive coverage
- Always verify scanner findings manually before reporting
- Use Burp's extension ecosystem for specialized testing

### Key Takeaways

- Configure Burp Scanner for the target application's data structures
- Use targeted scanning for efficiency
- Always verify scanner findings manually
- Understand Burp's insertion point configuration
