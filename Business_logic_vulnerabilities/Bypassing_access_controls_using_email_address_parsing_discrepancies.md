# Bypassing access controls using email address parsing discrepancies

### Goal -

Exploit a logic flaw in email address parsing to bypass access controls.

### Vulnerability / Concept

The application processes email addresses differently across components, creating a logic flaw that can be exploited to bypass access controls.

### Recon / Initial Analysis

1. Identify email address handling in the application
2. Test different email formats (RFC 5321, RFC 5322, Unicode)
3. Look for discrepancies in how different components parse the same email

### Exploitation

1. Identify the email parsing discrepancy
2. Craft an email address that is parsed differently by different components
3. Use the discrepancy to bypass access controls

### Why It Works

Different email parsing libraries may interpret the same email address differently. For example, `user@domain.com` and `user@domain.com.` (with trailing dot) may be treated as the same or different depending on the parser. This discrepancy can be exploited to bypass access controls.

### Key Takeaways

- Use consistent email parsing across all components
- Normalize email addresses before comparison
- Be aware of RFC ambiguities in email address formats
