# NoSQL Injection

NoSQL injection attacks exploit weaknesses in applications that use NoSQL databases. Unlike SQL injection, NoSQL injection can target both the syntax and structure of NoSQL queries, which often use JSON or JavaScript objects rather than string-based SQL queries.

NoSQL databases such as MongoDB, CouchDB, and Redis use different query languages, but they all accept structured data objects as input. When user input is incorporated into these objects without proper sanitization, attackers can manipulate the query logic to bypass authentication, extract data, or execute arbitrary code.

## Labs

- [Detecting NoSQL injection](./Detecting_NoSQL_injection.md)
- [Exploiting NoSQL injection to extract data](./Exploiting_NoSQL_injection_to_extract_data.md)
- [Exploiting NoSQL operator injection to bypass authentication](./Exploiting_NoSQL_operator_injection_to_bypass_authentication.md)
- [Exploiting NoSQL operator injection to extract unknown field names](./Exploiting_NoSQL_operator_injection_to_extract_unknown_field_names.md)
