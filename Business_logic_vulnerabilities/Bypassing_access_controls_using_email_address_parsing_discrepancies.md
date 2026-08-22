# Bypassing access controls using email address parsing discrepancies

### Goal -

Exploit a logic flaw in email address parsing to bypass access controls.

### Exploitation

1. Identify the email parsing discrepancy
2. Craft an email address that is parsed differently by different components
3. Use the discrepancy to bypass access controls

### Why It Works

The exploit succeeds because this lab validates email addresses to prevent attackers from registering addresses from unauthorized domains. there is a parser discrepancy in the validation logic and library used to parse email addr

The root cause is a failure in the application's security architecture specific to this logic flaws scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab validates email addresses to prevent attackers from registering addresses from unauthorized"
- Validate business-critical parameters server-side — never trust client-supplied values.

## PortSwigger Lab

**Official lab:** Bypassing access controls using email address parsing discrepancies

**PortSwigger:** https://portswigger.net/web-security/logic-flaws/examples/lab-logic-flaws-bypassing-access-controls-using-email-address-parsing-discrepancies
