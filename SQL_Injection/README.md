# SQL Injection

## Contents

- [SQLMap](./SQLMap.md)
- [SQL injection cheat sheet](./SQL_injection_cheat_sheet.md)
- [Examining the database](./Examining_the_database.md)
- [Visible error-based SQL injection](./Visible_error-based_SQL_injection.md)
- [SQL injection UNION attack, finding a column containing text](./SQL_injection_UNION_attack,_finding_a_column_containing_text.md)
- [Examining the database in SQL injection attacks.](./Examining_the_database_in_SQL_injection_attacks./README.md)

[https://www.akto.io/blog/sql-injection-cheat-sheet](https://www.akto.io/blog/sql-injection-cheat-sheet)

{% hint style="info" %}
💡 For a `UNION` query to work, two key requirements must be met:
{% endhint %}

  - The individual queries must return the same number of columns.
  - The data types in each column must be compatible between the individual queries.