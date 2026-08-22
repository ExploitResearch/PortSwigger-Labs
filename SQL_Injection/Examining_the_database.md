# Examining the database

### Goal -

Use SQL injection to examine the database structure by querying the database type and version, and listing the database contents.

### Exploitation

1. Identify the SQL injection point
2. Query the database type and version using database-specific syntax
3. List all tables in the database using `information_schema` (MySQL/PostgreSQL) or `all_tables` (Oracle)
4. List columns in the target table
5. Retrieve the data from the identified columns
