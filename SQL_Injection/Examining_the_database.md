# Examining the database

### Goal -

Use SQL injection to examine the database structure by querying the database type and version, and listing the database contents.

### Vulnerability / Concept

The application is vulnerable to SQL injection. By examining the database structure, an attacker can identify table names, column names, and data types to craft more effective injection payloads.

### Exploitation

1. Identify the SQL injection point
2. Query the database type and version using database-specific syntax
3. List all tables in the database using `information_schema` (MySQL/PostgreSQL) or `all_tables` (Oracle)
4. List columns in the target table
5. Retrieve the data from the identified columns

### Why It Works

Different databases have different metadata tables and syntax. By examining the database structure, the attacker can craft precise payloads to extract the desired data. The `information_schema` table in MySQL/PostgreSQL and `all_tables`/`all_tab_columns` in Oracle expose the full database structure.

### Key Takeaways

- Use parameterized queries to prevent SQL injection
- Restrict database user permissions (no access to information_schema)
- Implement input validation
- Use a WAF for defense in depth
