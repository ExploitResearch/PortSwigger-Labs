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


### Real-World Impact

An attacker could exploit business logic flaws to:
- Purchase items at reduced or negative prices
- Bypass multi-step workflows (checkout, authentication flows)
- Access functionality outside their privilege level
- Manipulate application state for financial gain
- Bypass rate limits and brute-force protections
- Cause inconsistent application behavior that leads to data corruption


### Remediation

- Implement server-side validation for all business-critical parameters (prices, quantities, roles)
- Never trust client-side values for pricing, permissions, or workflow state
- Enforce workflow sequence integrity server-side (don't rely on UI ordering)
- Use server-side state machines for multi-step processes
- Implement consistency checks for financial transactions
- Rate-limit based on business logic, not just request volume
- Test business logic thoroughly with negative test cases

### Key Takeaways

- Use consistent email parsing across all components
- Normalize email addresses before comparison
- Be aware of RFC ambiguities in email address formats
