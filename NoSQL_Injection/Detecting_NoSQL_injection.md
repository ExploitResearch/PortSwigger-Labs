# Detecting NoSQL injection

### Goal -

Solve the PortSwigger lab: Detecting NoSQL injection

### Vulnerability / Concept

NoSQL injection occurs when user-controlled input is incorporated into NoSQL database queries without proper sanitization. This can allow attackers to manipulate query logic, bypass authentication, or extract sensitive data.

### Recon / Initial Analysis

1. Identify input fields that interact with the database (login forms, search bars, API endpoints)
2. Test with NoSQL operators like `$ne`, `$gt`, `$regex` to check for injection points
3. Observe application behavior when injecting JSON objects vs. string values

### Exploitation

1. Identify the injection point in the application
2. Craft a NoSQL injection payload appropriate for the target database
3. Test the payload and analyze the response

### Why It Works

The vulnerability exists because the application passes user input directly into NoSQL query functions without validating that the input is a simple string value. By injecting MongoDB operators (prefixed with `$`), an attacker can alter the query logic to return unintended results.

### Key Takeaways

- Always validate input type (string vs. object) before passing to database queries
- Use parameterized queries or ORM methods that prevent operator injection
- Implement input allowlists that reject `$`-prefixed keys in JSON input
